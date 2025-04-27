# Aquiplicity 2025

**Aquiplicity 2025** is a sophisticated web-based image composition tool designed for creating composite images from multiple layers using a threshold-based pixel selection algorithm. Built with HTML5, CSS, and JavaScript, it leverages the HTML5 Canvas API to enable real-time image manipulation directly in the browser. The tool supports interactive editing features such as patching, blending, and gradient overlays, making it ideal for photographers, digital artists, and developers interested in image processing.

This repository contains the complete source code for Aquiplicity 2025 (Single Threshold - Original Resolution), a standalone application that processes images at their native resolution for maximum fidelity.

---

## Features

- **Threshold-Based Composition**: Combines multiple images by selecting pixels based on color differences, controlled by a user-defined threshold (1% to 100%).
- **Color Distancing**: Uses Euclidean distance in RGB space to quantify pixel differences, ensuring precise layer selection.
- **Interactive Editing**:
  - **Patch Click/Lasso**: Replace small regions or user-defined areas with pixels from another layer (Ctrl + click/drag).
  - **Blend Lasso**: Smooth regions by averaging neighboring pixels (Alt + click/drag).
  - **Gradient Lasso**: Apply semi-transparent color gradients for creative effects (Shift + click/drag).
- **Dynamic Layer Management**: Add up to 15 images and remove them at runtime with synchronized UI updates.
- **Undo System**: Supports up to 15 undo steps for edits like patching, blending, and gradients.
- **Image Saving**: Export composites as PNG files at original resolution.
- **Tracy Rose Preset**: Applies an optimized threshold (~13%) for balanced blending.
- **Responsive UI**: Adapts canvas size to screen constraints while maintaining pixel accuracy.
- **Status Feedback**: Real-time updates on processing, errors, and actions via a status bar.

---

## Demo

To try Aquiplicity 2025, open `index.html` in a modern web browser (see [Installation](#installation)). Upload multiple images, adjust the threshold, and explore the editing tools to create unique composites.

---

## Installation

Aquiplicity 2025 is a client-side application requiring no server setup. Follow these steps to run it locally:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/aquiplicity-2025.git
   cd aquiplicity-2025

----------------------------------------------------------------------
---=============   NOTES ABOUT HOW PIXELS ARE PATCHED =============---
----------------------------------------------------------------------

Aquiplicity code implements an image composition tool with a lasso-based patching system, replacing the original 4x4 pixel patching scheme that caused grid-like artifacts at certain angles. 

Let's analyze the current lasso patching scheme based on the provided code, focusing on the patchRegion and applyLassoPatch functions, which handle the patching operations.
Current Lasso Patching Scheme

The application now uses an area-based lasso patching system with the following characteristics:
Patch Click (No Modifier Key, Simple Click):

Function: patchRegion(clickX, clickY)

Behavior: When the user clicks on the canvas without holding any modifier keys (Ctrl, Alt, or Shift), a small square patch is applied centered at the click location.
Patch Size: Defined by PATCH_CLICK_SIZE = 4 pixels, creating a 4x4 pixel square region (16 pixels total).
Source Layer Selection: The layer to patch from is determined by the layerMatrix value at the exact pixel clicked (clickX, clickY). 
The layerMatrix stores indices of the source images used in the composition.

Operation:
The function calculates the top-left corner of the patch (startX, startY) by offsetting clickX and clickY by half the patch size (halfPatch = Math.floor(PATCH_CLICK_SIZE / 2) = 2).
It ensures the patch stays within the image bounds using Math.max and Math.min.
For each pixel in the 4x4 region, it copies the RGB and alpha values from the selected source image's ImageData to the masterImageData at the corresponding pixel.
The number of pixels patched is tracked and reported in the status (typically 16 pixels unless the click is near the image edge).

Example Status Message: Patched 16 pixels in 4x4 region from layer X at (clickX, clickY).

Purpose: This provides a precise, small-scale patching mechanism for quick touch-ups without requiring a lasso selection.
Patch Lasso (Ctrl + Drag):
Function: applyLassoPatch()

Behavior: When the user holds Ctrl and drags to draw a lasso (closed polygon), the area enclosed by the lasso is patched with pixels from a single source layer.

Area Selection:
The lasso is defined by an array of points (lassoPoints) collected during the drag operation.
The isPointInLasso(x, y, points) function uses the ray-casting algorithm to determine if a pixel's center (x + 0.5, y + 0.5) lies inside the lasso polygon.

Source Layer Selection:  ***************
The source layer is determined by the layerMatrix value at the starting point of the lasso (lassoPoints[0].x, lassoPoints[0].y).
This ensures the entire enclosed area is patched from the same layer as the initial click, providing consistent patching within the selected region.

Operation:
The function computes the bounding box of the lasso (minX, maxX, minY, maxY) to optimize processing by only checking pixels within this rectangle.
For each pixel in the bounding box, it checks if the pixel's center is inside the lasso using isPointInLasso.
If inside, it copies the RGB and alpha values from the selected source image's ImageData to the masterImageData at the corresponding pixel.
The number of pixels patched is tracked and reported.

After patching, the lasso is cleared, and the canvas is redrawn (clearLassoAndRedraw).
Example Status Message: Applied patch lasso from layer X (Y pixels).

Purpose: This allows for larger, irregularly shaped regions to be patched from a single source layer, avoiding the grid artifacts of the 4x4 scheme by using a freeform selection.
Key Differences from the 4x4 Pixel Patching Scheme...The original 4x4 pixel patching scheme applied patches in a grid-like pattern (e.g., dividing the image into 4x4 pixel blocks or applying patches at regular intervals), which caused visible grid artifacts at certain angles due to the regular, tiled nature of the patches. 

The new lasso-based scheme addresses this by using Freeform Selection:
The lasso allows users to define arbitrary, irregular shapes for patching, eliminating the regular grid pattern and reducing visible seams.

Flexible Patch Size: 
The patch click uses a small 4x4 pixel region for precision but is applied only where clicked, not across a grid.
The patch lasso can enclose areas of any size and shape, limited only by the user's drawing and the image bounds.
Single Layer Consistency: The patch lasso uses the layer at the lasso's starting point for the entire region, ensuring uniformity within the patched area and avoiding the patchwork effect of grid-based patching.

User Control: The lasso requires explicit user interaction (Ctrl + Drag), giving precise control over where and how patches are applied, unlike an automated grid-based approach.
Additional Notes on the Lasso Patching Scheme

Performance Optimization:
The applyLassoPatch function uses a bounding box to limit the pixels checked with isPointInLasso, improving performance for large images or complex lassos.
The isPointInLasso function is efficient for determining point inclusion (NOTE it may become a bottleneck for very large lassos or high-resolution images due to repeated calls)

Error Handling:
The code includes checks for invalid conditions (e.g., insufficient lasso points, invalid layer indices, or out-of-bounds coordinates) and provides appropriate status messages.
For example, if the lasso has fewer than 3 points, it is cancelled with a message: Lasso too small, action cancelled..

Visual Feedback:
During lasso drawing, redrawCanvasWithLasso renders a semi-transparent green fill (rgba(0, 255, 0, 0.3)) and a dark green stroke (rgba(0, 100, 0, 0.7)) to show the patch lasso's shape, enhancing user experience.
The lasso is cleared after application, ensuring a clean canvas.

Undo Support:
Both patch click and patch lasso actions save the masterImageData state to the historyStack before applying changes, allowing users to undo with Ctrl+Z or the Undo button.
**************** >> The history is limited to MAX_HISTORY = 15 states to manage memory.

Potential Artifacts and Considerations.  While the lasso patching scheme eliminates the grid artifacts of the 4x4 scheme, there are still scenarios where artifacts could occur

Sharp Edges: The patch lasso copies pixels directly from the source layer without blending, which could create noticeable edges if the source and target regions have significant color or texture differences. The applyLassoBlend function (Alt + Drag) can be used to smooth these transitions.

Layer Selection: Since the patch lasso uses the layer at the lasso's starting point, choosing an inappropriate starting point could result in an undesired source layer. Users must click carefully to select the intended layer.

Performance: For very large images or complex lassos, the pixel-by-pixel processing in applyLassoPatch might be slow, especially on lower-end devices.

In summary the current lasso patching scheme uses a 4x4 pixel patch for simple clicks and a freeform lasso-based area patch for Ctrl + Drag operations. It replaces the 4x4 grid-based patching to eliminate grid-like artifacts, offering precise, user-controlled patching with irregular shapes. The scheme is well-implemented with robust error handling, undo support, and visual feedback, making it suitable for detailed image composition tasks.

