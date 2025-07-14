    Aquiplicity 2025 - JavaScript Image Stacking and Compositing Tool for clone images

Aquiplicity 2025 is a browser-based image compositing tool built with HTML5, CSS, and JavaScript. It enables users to upload multiple images, composite them using a single-threshold algorithm, and interactively refine the output using lasso-based and brush-based editing tools. The tool supports advanced features like undo, dynamic brush sizing, and gradient overlays, making it suitable for creative image manipulation tasks.
Table of Contents

Features (#features)
Demo (#demo)
Installation (#installation)
Usage (#usage)
How It Works (#how-it-works)
Technical Details (#technical-details)
File Structure (#file-structure)
Contributing (#contributing)
Known Issues (#known-issues)
Future Enhancements (#future-enhancements)
License (#license)
Acknowledgements (#acknowledgements)

Features:

=- Image Upload and Management:
Upload multiple images (up to 15) via a file input.

=- Display thumbnails in a scrollable sidebar with metadata (layer index, filename, dimensions).

=- Remove individual images with a clickable "X" button on thumbnails.

=- Image Compositing:
Automatic compositing of multiple images using a single-threshold algorithm based on color distance.

=- Adjustable threshold slider (0.01% to 100% difference) for fine-tuning composition sensitivity.

=- "Tracy Rose" preset for quick threshold configuration (~13%).

Interactive Editing:

=- Patch Lasso (Ctrl+Drag): Select a region to replace with pixels from the layer at the starting point.

=- Blend Lasso (Alt+Drag): Apply a feathering effect within a selected region using a 2-pixel radius.

=- Gradient Lasso (Shift+Drag): Overlay a gradient based on sampled colors within the selected region (25% opacity).

=- Patch Brush Click: Click to apply a circular patch from the layer at the click point, with adjustable brush size (4px to 200px).

Undo and Reset:
=- Undo up to 15 actions (e.g., lasso applications, brush clicks).

=- Reset the application to clear all images, canvas, and settings.

Canvas and Output:
=- Responsive canvas that fits images to the screen while preserving aspect ratio.

=- Save the composed image as a PNG file with a default filename (Aquiplicity_Master_BrushClick.png).

User Interface:
=- Marquee with instructions for quick reference.

=- Status bar for real-time feedback (e.g., processing progress, errors).

=- Responsive layout with a thumbnail strip, controls, and working area.

=- Smooth animations and hover effects for buttons and thumbnails.

Keyboard Shortcuts:
Ctrl+Z or Cmd+Z for undo.

Demo
To see Aquiplicity 2025 in action:
Clone the repository.

Open index.html in a modern web browser (e.g., Chrome, Firefox).

Upload multiple images and experiment with the compositing and editing tools.

A live demo may be hosted in the future (see Future Enhancements (#future-enhancements)).
Installation
No external dependencies or server setup are required since Aquiplicity 2025 is a client-side application.
Prerequisites
A modern web browser (Chrome, Firefox, Edge, or Safari).

Basic knowledge of HTML and JavaScript for development or customization.

Steps
Clone the Repository:
bash

git clone https://github.com/TracyLeeRose/aquiplicity-2025.git
cd aquiplicity-2025

Serve the Application:
Option 1: Open index.html directly in a browser (e.g., file://path/to/aquiplicity-2025/index.html).

Option 2: Use a local server to avoid CORS issues with file inputs:
bash

npx http-server

Then navigate to http://localhost:8080.

Verify:
Ensure the UI loads with a marquee, controls, thumbnail strip, and canvas.

Upload images to confirm functionality.

Usage
Upload Images:
Click the file input to select multiple images (PNG, JPEG, etc.).

Images are resized to match the first image’s dimensions and displayed as thumbnails.

Automatic Compositing:
If two or more images are uploaded, compositing starts automatically.

Adjust the Threshold Slider to control how color differences affect layer selection (default: 15%).

Click Compose! to recomposite with the current threshold.

Edit the Composition:
Patch Lasso (Ctrl+Drag): Draw a region to patch with pixels from the layer at the starting point.

Blend Lasso (Alt+Drag): Draw a region to apply a feathering effect.

Gradient Lasso (Shift+Drag): Draw a region to overlay a gradient.

Patch Brush Click: Click to apply a circular patch with adjustable size (use the Brush Size Slider).

Manage Layers:
Remove images by clicking the "X" on thumbnails.

Thumbnails update dynamically with layer indices and metadata.

Save or Undo:
Click Save Master Image to download the composed image.

Click Undo or press Ctrl+Z to revert changes.

Click Reset to clear everything and start over.

Use Presets:
Click By Tracy Rose to apply a predefined threshold (~13%).

How It Works
Aquiplicity 2025 composites images by comparing pixel color differences against a user-defined threshold. It then allows interactive editing via lasso and brush tools.
Compositing Algorithm
Image Loading:
Images are loaded into an ImageStack class, resized to match the first image’s dimensions.

Each image is converted to ImageData for pixel-level processing.

Smoothing:
Each layer is smoothed (6 iterations) to reduce noise, using a 4-neighbor averaging filter.

Threshold-Based Compositing:
For each pixel, the smoothed color of the base layer (first image) is compared to other layers.

If the color distance (Euclidean distance in RGB space) exceeds the threshold, the pixel is taken from the highest-indexed layer meeting the condition.

The result is a masterImageData (composed image) and a layerMatrix (indicating which layer each pixel came from).

Interactive Editing:
Patch Lasso/Brush: Copies pixels from the layer indicated by the layerMatrix at the starting point or click location.

Blend Lasso: Averages pixels within a 2-pixel radius inside the lasso for a feathering effect.

Gradient Lasso: Samples colors at the lasso’s edges to create a linear gradient overlay.

User Interface
Marquee: Displays instructions (e.g., “Patch (Ctrl+Drag) / Blend (Alt+Drag)”).

Controls: Includes file input, sliders, and buttons for compositing, undoing, resetting, and saving.

Thumbnail Strip: Shows image previews with remove buttons.

Canvas: Displays the composed image and supports lasso drawing and brush clicks.

Status Bar: Provides real-time feedback (e.g., “Processing pixels... (50%)”).

Technical Details
Architecture
HTML Structure:
A single index.html file with embedded CSS and JavaScript.

Layout: Marquee, controls, thumbnail strip, and working area with a canvas.

CSS:
Flexbox-based responsive layout.

Custom styles for buttons, sliders, thumbnails, and canvas.

Hover and active states for interactive elements.

JavaScript:
ImageStack Class:
Manages image loading, smoothing, and compositing.

Methods: addImage, smoothLayer, colorDistance, compose.

Global State:
Variables like masterImageData, layerMatrix, lassoPoints, and historyStack.

Event Handlers:
Canvas events for lasso drawing and brush clicks.

Global mouse events for lasso completion.

Keyboard shortcuts for undo.

Utility Functions:
fitToScreen: Scales canvas to fit the working area.

updateStatus: Displays messages and errors.

saveStateForUndo: Stores image states for undo.

Key Components
Canvas: Uses the 2D context (willReadFrequently: true) for efficient pixel operations.

Sliders:
Threshold: Maps 0.01–1.0 to 0.01%–100% for color difference.

Brush Size: Adjustable from 4px to 200px for patch brush clicks.

Undo System:
Stores up to 15 ImageData states in historyStack.

Triggered by lasso applications, brush clicks, or image removal.

Lasso System:
Stores points in lassoPoints and uses a point-in-polygon algorithm (isPointInLasso).

Supports three modes: patch, blend, and gradient.

Performance Considerations
Image Size:
Warns for resolutions above 4000x4000 pixels due to memory and performance concerns.

Resizes images to match the first image’s dimensions.

Smoothing:
Uses Float32Array for precision during smoothing iterations.

Processes pixels asynchronously with setTimeout to prevent UI freezing.

Compositing:
Reports progress every 5% to keep the UI responsive.

Uses Uint8ClampedArray for efficient pixel manipulation.

File Structure

aquiplicity-2025/
├── index.html       # Main application file (HTML, CSS, JavaScript)
├── README.md        # This documentation
└── LICENSE          # License file (to be added)

Contributing
Contributions are welcome! To contribute:
Fork the Repository:
bash

git fork https://github.com/your-username/aquiplicity-2025.git

Create a Feature Branch:
bash

git checkout -b feature/your-feature-name

Make Changes:
Follow the existing code style (e.g., consistent indentation, descriptive variable names).

Update documentation for new features or changes.

Test thoroughly in multiple browsers.

Submit a Pull Request:
Push your branch to your fork.

Open a PR with a detailed description of your changes.

Contribution Ideas
Add support for additional image formats (e.g., WebP).

Implement zoom/pan for the canvas.

Enhance the undo system to include redo functionality.

Optimize performance for large images.

Known Issues
Large Images:
Images above 4000x4000 pixels may cause slow performance or memory issues.

Mitigation: Warns users and suggests resizing images beforehand.

Canvas Tainting:
Saving may fail if images cause canvas tainting (e.g., cross-origin issues).

Workaround: Use a local server to serve files.

Lasso Cancellation:
Releasing the modifier key (Ctrl/Alt/Shift) before mouse-up cancels the lasso, which may confuse users.

Browser Compatibility:
Not tested extensively on older browsers (e.g., IE) or mobile devices.

Future Enhancements
Mobile Support:
Add touch events for lasso and brush interactions.

Optimize layout for smaller screens.

Advanced Editing Tools:
Support for freehand drawing or shape-based selections.

Add color adjustment or filter options.

Redo Functionality:
Extend the undo system to include redo actions.

Live Demo:
Host a demo on GitHub Pages or a similar platform.

Export Options:
Allow saving in JPEG or WebP formats.

Export layer matrices or project files for later editing.

License
This project is licensed under the MIT License. See the LICENSE file for details.
Acknowledgements
Tracy Rose: Inspiration for the preset threshold setting.

HTML5 Canvas: For enabling powerful in-browser image manipulation.

Open Source Community: For tools and libraries that make projects like this possible.

