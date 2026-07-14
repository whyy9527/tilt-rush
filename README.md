# Tilt Rush V1

The frozen top-down edition of Tilt Rush, an open-source browser racing game controlled with head movement through a webcam. Lean to steer, flick upward to jump traffic, or use the keyboard fallback.

The annotated `v1.0.0` tag is the source of truth for this completed edition. Active development after that tag belongs to the separate first-person V2 line.

## Play

Open the GitHub Pages deployment, choose **Enable camera**, complete the short neutral-position calibration, and start a run.

- Lean left/right: steer
- Flick upward: jump
- Arrow keys: keyboard steering
- Space: keyboard jump
- F: fullscreen

Camera frames are processed locally in the browser with MediaPipe Face Landmarker and are never uploaded by this project.

## Run locally

Camera access requires a secure context. Localhost is accepted by browsers:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Architecture

Tilt Rush V1 is a static top-down Canvas game: one HTML entry point plus raster assets. It has no backend, account system, analytics, or headphone integration. MediaPipe is loaded from jsDelivr and its face model from Google Storage when camera control is enabled.

## License

MIT. See [LICENSE](LICENSE).
