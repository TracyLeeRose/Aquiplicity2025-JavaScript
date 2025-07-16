# Aquiplicity 2025: The Industrial Art Composer by Tracy Rose

![Aquiplicity 2025 UI](https://i.imgur.com/gD4iZkL.png)

Aquiplicity 2025 is a powerful, browser-based digital art tool that allows users to compose and blend multiple images into a single, unique piece of art. It uses a sophisticated color-difference algorithm to create a base composition, which can then be artistically modified in real-time using an intuitive suite of brush and lasso tools. The entire application runs client-side with zero dependencies, written in pure HTML, CSS, and JavaScript.

---

## ✨ Core Features

*   **Layer-Based Image Composition:** Load multiple images which are treated as layers. The first image forms the base.
*   **Threshold-Based Blending:** An intelligent algorithm compares each pixel of the upper layers to the base layer. If a pixel's color difference is above a user-defined **Threshold**, it's chosen for the final image.
*   **Interactive Patch Brush:** The main creative tool. Click and draw on the canvas to "paint" pixels from an underlying source layer onto the master image, determined by the composition's `layerMatrix`.
*   **Advanced Lasso Tools:**
    *   **Patch Lasso (`Ctrl + Drag`):** Fill a free-form area with pixels from a single source layer.
    *   **Blend/Feather Lasso (`Alt + Drag`):** Apply a smoothing blur effect to the pixels within a selected area.
    *   **Gradient Overlay Lasso (`Shift + Drag`):** Apply a beautiful, semi-transparent color gradient to a selected area.
*   **Real-time Previews:** The brush tool shows a live, translucent preview of your stroke, and lasso tools show the selection area as you draw.
*   **Multi-Level Undo:** Made a mistake? Undo your brush strokes and lasso applications with `Ctrl+Z` or the Undo button.
*   **No Server Needed:** The entire application runs in your web browser. There's no backend, no data is uploaded, and no installation is required.
*   **Theming:** Switch between a clean Light Mode and a focused Dark Mode.

---

## 🔧 How It Works: The Technical Guts

The power of Aquiplicity lies in its core composition logic and the data structures it uses to enable real-time editing.

### 1. The `ImageStack` Class

This class is the heart of the application. It manages all loaded images.
*   When an image is added, it's drawn onto an internal canvas and its pixel data is extracted as an `ImageData` object.
*   All images are automatically resized to match the dimensions of the first image loaded, ensuring consistency.
*   It stores an array of these `ImageData` objects, which serve as the "layers".

### 2. The Composition Algorithm

When you click the **Compose!** button, the following process occurs:

1.  **Smoothing:** To reduce noise and create more cohesive regions, each layer's `ImageData` is first run through a simple box-blur smoothing filter. This prevents stray, noisy pixels from dominating the final composition.
2.  **Pixel Iteration:** The algorithm iterates through every single pixel coordinate `(x, y)` of the canvas.
3.  **Color Distance Calculation:** For each pixel, it takes the color from the smoothed base layer (Layer 0) as a reference. It then compares this color to the color of the corresponding pixel in the layers above it, starting from the topmost layer and working down (`Layer N-1` -> `Layer 1`). The comparison is a standard Euclidean distance in RGB color space: `sqrt((r2-r1)² + (g2-g1)² + (b2-b1)²)`.
4.  **Threshold Check:** If the calculated color distance is **greater** than the user-defined `Threshold`, the algorithm considers this pixel "sufficiently different." It stops searching and selects this layer as the source for the final pixel.
5.  **Pixel Assignment:** The original, non-smoothed pixel data from the chosen source layer is copied to the `masterImageData`. If no layer's pixel meets the threshold, the pixel from the original base layer (Layer 0) is used.
6.  **The `layerMatrix`:** Crucially, as each pixel is decided, its source layer index is stored in a `Uint8Array` called the `layerMatrix`. This matrix has the same dimensions as the image and acts as a "map," remembering which layer contributed every single pixel to the master image.

### 3. The Interactive Tools

The `layerMatrix` is the key that unlocks the powerful interactive tools.

*   **Patch Brush & Patch Lasso:** When you begin a brush stroke or lasso, the tool performs a lookup in the `layerMatrix` at your starting mouse coordinates `(x, y)`. This tells it the source layer index for that specific spot. The tool then uses that layer index as the source for the *entire* patch operation, ensuring a consistent and predictable result as you paint or select.
*   **Other Tools:** The Blend and Gradient tools operate directly on the pixels of the `masterImageData` within the bounds of the user-drawn lasso.

---

## 🚀 How to Use

### Getting Started

1.  Click the **Image Input** button to load two or more images.
2.  The software will automatically perform an initial composition.
3.  Adjust the **Threshold** slider to control how much of the upper layers are blended in. A lower threshold is more selective; a higher threshold is less selective.
4.  Click **Compose!** to see the changes.

### The Creative Tools

Your primary interaction happens on the main canvas.

| Tool                  | Action                 | Description                                                                                             |
| --------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------- |
| **Patch Brush**       | `Click + Drag`         | Paints with a translucent pink preview. On release, it fills the stroke with pixels from the source layer under your initial click point. Adjust size with the **Brush Size** slider. |
| **Patch Lasso**       | `Ctrl + Drag`          | Draws a free-form shape. On release, it fills the area with pixels from the source layer under your starting point. |
| **Blend/Feather Lasso** | `Alt + Drag`           | Draws a free-form shape. On release, it applies a gentle blur to all pixels inside the area, softening edges. |
| **Gradient Lasso**    | `Shift + Drag`         | Draws a free-form shape. On release, it applies a semi-transparent color gradient across the selected area. |
| **Undo**              | `Ctrl + Z` / `Undo` Button | Reverts the last brush or lasso action you completed.                                                     |

---

## 💻 Running Locally

No build process or dependencies are required.

1.  Clone this repository to your local machine:
    ```bash
    git clone https://github.com/your-username/aquiplicity-2025.git
    ```
2.  Navigate to the directory:
    ```bash
    cd aquiplicity-2025
    ```
3.  Simply open the `index.html` file in a modern web browser like Chrome, Firefox, or Edge.

> **Note:** For the best experience, it's recommended to use a simple local server (like the "Live Server" extension for VS Code) to avoid any potential browser security restrictions related to loading files directly from the local filesystem (`file:///`).

## 🛠️ Technology Stack

*   **HTML5:** For the core structure of the application.
*   **CSS3:** For all styling, including a modern themeable design using CSS Variables.
*   **Vanilla JavaScript (ES6+):** All application logic, DOM manipulation, and canvas interactions are written in pure JavaScript with no external libraries or frameworks.
