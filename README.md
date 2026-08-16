# ASCIIVID

ASCIIVID is an interactive, browser-based ASCII animation and video export tool. It renders a complex stick-figure action sequence entirely in real-time using HTML5 Canvas and procedural ASCII character mapping.

## Features

- **High-Fidelity ASCII Rendering**: Uses a dual-canvas pipeline to sample high-resolution graphics and map them to a dense grid of ASCII characters based on luminance.
- **Dynamic Choreography (35s Sequence)**: 
  - An action-packed sequence featuring a runner leaping with a 360-degree front flip.
  - Knockout parkour mechanics with physics-based recoils and dust particles.
  - Humorous details like a wagging tongue animation to mock chasers.
  - Spiderman swinging in to pull down a web curtain, seamlessly cross-fading into a sprawling red ASCII web.
  - Interactive "book-ends" with a virtual cursor swooping in to click a PLAY button to start, and an X button to finish with a cinematic fade-to-black.
- **Procedural Animations**: Characters are drawn procedurally with physics-based kinematics (`kfOvershoot`), gait cycles (`gaitAngles`), and camera shake impacts.
- **Perfect Fixed-Framerate Export**: Replaces standard `MediaRecorder` with a raw **WebCodecs + WebMMuxer API pipeline**. This steps mathematically frame-by-frame (bypassing realtime stutters) to encode a flawless, zero-dropped-frame `50 Mbps` VP9 WebM video.
- **Interactive Scrubber**: Fully controllable timeline scrubber with frame-by-frame precision.

## Running Locally

Because the project relies on drawing an external image (`poster.jpg`) to a canvas, it requires a local web server to bypass CORS restrictions. Without a server, drawing a local image taints the canvas, throwing a `SecurityError` during export.

1. Ensure you have Python installed.
2. Open a terminal in the project directory.
3. Run `python -m http.server 8080` (or your preferred local server).
4. Navigate to `http://localhost:8080/asciivid.html` in your browser.
5. *(Optional)* Alternatively, you can click the "UPLOAD POSTER" button in the UI to securely load a local image without triggering CORS errors.

## Exporting

1. Click the "PLAY" button to start the animation.
2. Wait for the 35.0-second animation to complete, or use the scrubber to jump to the end.
3. Click "EXPORT" to start the offline encoding pipeline.
4. The engine will pause real-time playback and render mathematically frame-by-frame (indicated by a % loader). 
5. The high-quality `TinkerHub_Orientation_ASCII_HQ.webm` file will automatically download.

## Architecture

- **`mainCanvas`**: The high-resolution canvas that renders the final ASCII text grid.
- **`sceneCanvas`**: A hidden offscreen canvas where the actual shapes, colors, and animations are drawn procedurally.
- **`renderAscii()`**: The core engine that scans `sceneCanvas` pixel by pixel, calculates luminance, maps it to an ASCII character, and writes it to `mainCanvas`.
- **`WebCodecs VideoEncoder`**: Encodes the raw pixels of `mainCanvas` directly into a WebM stream, bypassing real-time dropping issues.

---
Made by [Lunarmist-byte](https://github.com/Lunarmist-byte) | [LinkedIn](https://www.linkedin.com/in/amal-s-kumar-ba69a1290/)
