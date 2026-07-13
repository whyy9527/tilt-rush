# Tilt Rush

An open-source browser racing experiment controlled with head movement through a webcam. Lean to steer, flick upward to jump traffic, or use the keyboard fallback.

## Play

Open the GitHub Pages deployment, choose **Enable camera**, complete the short neutral-position calibration, and start a run.

- Lean left/right: steer
- Flick upward: jump
- Arrow keys: keyboard steering
- Space: keyboard jump
- V: switch first-person/top-down view
- F: fullscreen

Camera frames are processed locally in the browser with MediaPipe Face Landmarker and are never uploaded by this project.

## Run locally

Camera access requires a secure context. Localhost is accepted by browsers:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Architecture

Tilt Rush is a static web game: one HTML entry point plus raster assets. It has no backend, account system, analytics, or headphone integration. MediaPipe is loaded from jsDelivr and its face model from Google Storage when camera control is enabled.

## License

MIT. See [LICENSE](LICENSE).
