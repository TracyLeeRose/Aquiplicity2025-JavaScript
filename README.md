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
