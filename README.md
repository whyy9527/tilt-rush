# Tilt Rush V2

The active first-person edition of Tilt Rush, an open-source browser racing game controlled with head movement through a webcam. Lean to steer, flick upward to jump traffic, or use the keyboard fallback.

The completed top-down V1 is maintained at the annotated `v1.0.4` tag. Active `main` development is the separate first-person V2 line.

## Play

Open the GitHub Pages deployment, allow the automatic camera request, complete the short neutral-position calibration, and start a run. Mobile browsers that block automatic preview playback show a `Start camera` action without requesting permission again. If camera access is denied or unavailable, keyboard controls remain active and the camera can be retried from the control deck.

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

Tilt Rush V2 is a static Three.js first-person game: one HTML entry point, one WebGL canvas, and raster assets. Traffic and camera travel share the generated course's logical-to-world distance scale. It has no backend, account system, analytics, or headphone integration. Three.js and MediaPipe are loaded from jsDelivr; the face model is loaded from Google Storage when camera control is enabled.

## License

MIT. See [LICENSE](LICENSE).
