markdown
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
Serve the Application:
Option 1: Local File Access:
Open index.html directly in a modern browser (e.g., Chrome, Firefox, Edge). Note: Some browsers may restrict file input due to security policies when opened via file://.
Option 2: Local Web Server (recommended):
Use a simple HTTP server to avoid CORS issues:
bash
python3 -m http.server 8000
Then navigate to http://localhost:8000 in your browser.
Dependencies:
No external libraries are required. The application uses vanilla JavaScript and standard HTML5/CSS3.
Ensure your browser supports the HTML5 Canvas API and modern JavaScript (ES6+).
Usage
Launch the Application:
Open index.html in a browser. The interface includes:
A control panel (top) with upload, compose, undo, reset, and threshold controls.
A thumbnail strip (left) showing uploaded images.
A canvas (center) displaying the composite image.
A status bar (bottom) for feedback.
Upload Images:
Click "Choose Files" to select multiple images (JPEG, PNG, etc., up to 15).
Images load automatically, with thumbnails appearing in the left strip.
If two or more images are uploaded, composition starts immediately.
Adjust Threshold:
Use the "Threshold (% Diff)" slider (1% to 100%, default 15%) to control pixel selection.
Lower values favor the base image; higher values mix more layers.
Click "Compose!" to recompose with the new threshold.
Edit the Composite:
Patch Click: Click on the canvas to swap a 2x2 pixel region with another layer’s pixels.
Patch Lasso: Hold Ctrl, click, and drag to define a region, then release to patch from another layer.
Blend Lasso: Hold Alt, click, and drag to smooth a region.
Gradient Lasso: Hold Shift, click, and drag to apply a gradient overlay (25% opacity).
Release modifier keys after the mouse to cancel actions.
Remove Images:
Hover over a thumbnail and click the red "X" to remove it.
Remaining thumbnails update automatically; recompose if needed.
Undo Edits:
Click "Undo" or press Ctrl+Z to revert the last edit (up to 15 steps).
Undo is disabled during composition or after image removal.
Save Your Work:
Click "Save Master Image" to download the composite as Aquiplicity_Master_OrigRes.png.
Reset:
Click "Reset" to clear all images, edits, and settings, returning to the initial state.
Tracy Rose Preset:
Click "By Tracy Rose" to set the threshold to ~13%, then "Compose!" to apply.
Technical Details
Architecture
Frontend: Single HTML file (index.html) with embedded CSS and JavaScript.
Core Logic: The ImageStack class manages image data, composition, and color distancing.
Canvas Rendering: Uses a 2D canvas context with willReadFrequently: true for optimized pixel access.
Event Handling: Mouse and keyboard events drive interactive editing, with modifier keys (Ctrl, Alt, Shift) for lasso modes.
Composition Algorithm
Input: Multiple ImageData objects (RGBA, same dimensions).
Process:
Smooth each layer using a 4-neighbor averaging filter (6 iterations) to reduce noise.
For each pixel, compute Euclidean RGB distances between the smoothed base layer and other layers.
Select the first layer (highest index) where distance exceeds the threshold (scaled to 0–255), or default to the base layer.
Copy the original pixel from the selected layer to the output.
Store the layer index in a layerMatrix for editing.
Output: Composite ImageData and layerMatrix (Uint8Array).
Color Distancing
Metric: Euclidean distance in RGB space:
D = \sqrt{(r_1 - r_2)^2 + (g_1 - g_2)^2 + (b_1 - b_2)^2}
Role: Determines pixel selection by comparing smoothed layers against the threshold.
Editing Features
Patch Click: Copies a 2x2 region from the layer indicated by layerMatrix.
Patch Lasso: Uses ray-casting to identify pixels within a user-drawn polygon, replacing them with pixels from the starting point’s layer.
Blend Lasso: Averages pixels within a 5x5 window (radius 2) inside the lasso.
Gradient Lasso: Samples colors at lasso edges, interpolates linearly, and blends at 25% opacity.
Performance
Complexity:
Composition: 
O(W \times H \times L \times I)
, where 
W \times H
 is resolution, ( L ) is layers, ( I ) is smoothing iterations.
Lasso operations: 
O((maxX - minX) \times (maxY - minY) \times P)
, where ( P ) is lasso points.
Memory: Each layer uses 
W \times H \times 4
 bytes; undo history adds up to 15x this per state.
Optimizations: Asynchronous updates, bounding box checks, early termination in distance calculations.
File Structure
aquiplicity-2025/
├── index.html        # Main application (HTML, CSS, JavaScript)
└── README.md         # This file
index.html: Contains the entire application, including:
HTML: UI structure (canvas, controls, thumbnails).
CSS: Styles for responsive layout, buttons, and lasso visualizations.
JavaScript: Core logic (ImageStack), event handlers, and rendering.
Building and Contributing
Aquiplicity 2025 is a standalone project with no build step. To contribute:
Fork the Repository:
bash
git clone https://github.com/your-username/aquiplicity-2025.git
cd aquiplicity-2025
Make Changes:
Edit index.html for HTML/CSS/JavaScript modifications.
Test locally using a web server (see Installation (#installation)).
Submit a Pull Request:
Push changes to your fork.
Open a PR with a clear description of the feature, bug fix, or improvement.
Contribution Ideas
Add support for CIELAB/HSV color spaces for perceptually uniform distancing.
Implement adaptive thresholding or per-region controls.
Optimize performance with WebGL or Web Workers.
Enhance gradient lasso with user-defined opacity or non-linear interpolation.
Extend undo to persist across image removals.
Limitations
Color Space: RGB-based distancing is not perceptually uniform, potentially affecting blend quality.
Performance: Large images (>4000x4000) or many layers may slow down in browsers.
Threshold: Single global threshold limits spatial adaptability.
Undo: Cleared after image removal, limiting reversibility.
Browser Dependency: Relies on Canvas API; performance varies by browser.
License
This project is licensed under the MIT License. See the LICENSE file for details.
Acknowledgments
Inspired by advanced image compositing techniques in professional software.
Special thanks to the "Tracy Rose" preset, named for its creator’s contribution to optimal threshold settings.
Built with vanilla JavaScript to demonstrate the power of browser-based image processing.
Contact
For questions, bug reports, or feature requests, open an issue on GitHub or contact the maintainer at [your-email@example.com (mailto:your-email@example.com)].
Happy compositing with Aquiplicity 2025! 🎨

**Notes**:
- Replace `your-username` and `your-email@example.com` with your actual GitHub username and contact email.
- Add a `LICENSE` file to the repository if you choose to include one (e.g., MIT License).
- The README assumes the repository will be hosted on GitHub. Adjust URLs if using another platform.
- The structure follows GitHub conventions, balancing user-friendliness with technical depth for developers.
