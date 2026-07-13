# Tilt Rush

An open-source, first-person browser racing experiment controlled with head movement through a webcam. Lean to steer, flick upward to jump traffic, or use the keyboard fallback.

## Philosophy

Tilt Rush starts with a simple belief: head movement can be an expressive game input, not a novelty accessibility toggle. The game should still be fun with a keyboard; camera control should then make steering, leaning, and jumping feel more physical.

- **Gameplay before spectacle.** Speed must come from readable roads, close decisions, and responsive movement—not a crowded HUD or decorative noise.
- **The browser is the platform.** A link should be enough to play. Camera processing stays local, deployment stays static, and no account or backend is required.
- **One game, one simulation.** First-person and top-down views share the same track, physics, traffic, scoring, and input state. We do not maintain separate game versions for each camera.
- **Motion without discomfort.** Head movement controls the vehicle; it does not rotate the player's entire world. Camera roll, shake, and FOV effects must remain restrained and testable.
- **Open and editable.** The project favors understandable systems, owned or clearly licensed assets, and issue records that explain why a decision was made.

## Goals

1. Make first-person riding the primary experience, with top-down retained as a secondary and debugging view.
2. Replace the current hand-built perspective renderer with Three.js while preserving camera calibration, controls, scoring, progression, and local best scores.
3. Build tracks with real curves, elevation, sight lines, and staged difficulty instead of decorating a single straight road.
4. Make leaning, overtaking, jumping, landing, and collisions visually legible from the rider's point of view.
5. Keep the game fast to load, playable from GitHub Pages, and usable with either webcam or keyboard controls.

Tilt Rush is not trying to be a vehicle simulator, a backend multiplayer service, or an AirPods integration demo. AirPods input remains a separate project in [PodsInput](https://github.com/whyy9527/pods-input).

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

Tilt Rush is currently a static Canvas game: one HTML entry point plus raster assets. It has no backend, account system, analytics, or headphone integration. MediaPipe is loaded from jsDelivr and its face model from Google Storage when camera control is enabled.

The chosen direction is to keep the browser-native application and replace only its rendering layer with Three.js. Game rules and input remain engine-independent. See [issue 0001](issues/0001-threejs-first-person-renderer.md) for the first migration slice and [issues/README.md](issues/README.md) for the project lifecycle.

## License

MIT. See [LICENSE](LICENSE).
