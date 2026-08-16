# ASCIIVID

ASCIIVID is an interactive, browser-based ASCII animation and video export tool. It renders a complex stick-figure action sequence entirely in real-time using HTML5 Canvas and procedural ASCII character mapping.

## Features

- **High-Fidelity ASCII Rendering**: Uses a dual-canvas pipeline to sample high-resolution graphics and map them to a dense grid of ASCII characters based on luminance.
- **Dynamic Choreography**: A 34-second action-packed sequence featuring a runner, chasers, Spiderman pulling a curtain, and dynamic parkour/knockout mechanics.
- **Procedural Animations**: Characters are drawn procedurally with physics-based kinematics (`kfOvershoot`), gait cycles (`gaitAngles`), and camera shake impacts.
- **High-Quality Export**: Integrated `MediaRecorder` allows for direct export of the animation to a high-quality (50 Mbps) WebM video file, ensuring crisp text and perfect sync.
- **Interactive Scrubber**: Fully controllable timeline scrubber with frame-by-frame precision.

## Running Locally

Because the project relies on drawing an external image (`poster.jpg`) to a canvas, it requires a local web server to bypass CORS restrictions.

1. Ensure you have Python installed.
2. Open a terminal in the project directory.
3. Run `python -m http.server 8080` (or your preferred local server).
4. Navigate to `http://localhost:8080/asciivid.html` in your browser.

## Exporting

1. Click the "PLAY" button to start the animation.
2. Wait for the 34-second animation to complete.
3. Once finished, the "PLAY" button will become an "EXPORT" button.
4. Click "EXPORT" to download the high-quality `ascii_animation.webm` file.

## Architecture

- **`mainCanvas`**: The high-resolution canvas that renders the final ASCII text grid.
- **`sceneCanvas`**: A hidden offscreen canvas where the actual shapes, colors, and animations are drawn procedurally.
- **`renderAscii()`**: The core engine that scans `sceneCanvas` pixel by pixel, calculates luminance, maps it to an ASCII character, and writes it to `mainCanvas`.

---
Made by [Lunarmist-byte](https://github.com/Lunarmist-byte) | [LinkedIn](https://www.linkedin.com/in/amal-s-kumar-ba69a1290/)
