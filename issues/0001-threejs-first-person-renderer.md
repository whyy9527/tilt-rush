📌 # Establish the Three.js first-person renderer

Created: 2026-07-13
Source: Engine decision following the first-person V1 evaluation
Owner repo: `tilt-rush`
Related issues: [0002](0002-curved-elevated-track.md), [0003](0003-threejs-rider-steering.md)

## Goal

Replace the default Canvas pseudo-perspective view with a Three.js `PerspectiveCamera` rendering a static gray-box straight, while leaving the existing game state and normalized input contract unchanged.

## Context

The current first-person view projects top-down coordinates into a road-shaped Canvas polygon. Three.js is the chosen rendering layer, but renderer setup must land before track geometry and rider motion are added.

## Chosen Slice

When the first-person view renders, use one Three.js scene, perspective camera, and WebGL renderer to draw a static straight road inside the existing game shell.

## Scope

- Load Three.js from a browser-compatible ESM CDN without adding a build step.
- Add a dedicated WebGL canvas for one scene, `PerspectiveCamera`, and `WebGLRenderer` while retaining the existing Canvas element for top-down debug rendering.
- Render a visible gray-box straight, road boundaries, and depth markers.
- Make Three.js the default first-person render path.
- Preserve the Canvas top-down debug view, HUD, menu, resize, input, and game-state update paths.
- Expose the active renderer and camera type through `window.render_game_to_text()`.

## Non-goals

- Curves, elevation, course-relative motion, or course completion changes.
- Rider cockpit, steering visualization, camera lean, traffic, collision, or jump rendering in Three.js.
- Final models, textures, lighting polish, or a new build tool.
- Webcam contract changes.

## Acceptance Criteria

- [ ] The default first-person view renders through Three.js with a `PerspectiveCamera` and does not call `renderFirstPerson()`.
- [ ] A straight gray road, both road boundaries, and repeated depth markers are visible.
- [ ] Switching views shows only the active renderer canvas, and both views remain usable.
- [ ] Resize and fullscreen continue to fill the viewport without stretching the Three.js camera.
- [ ] `window.render_game_to_text()` reports `rendering.renderer: "three"` and `rendering.camera: "PerspectiveCamera"` in first-person mode.
- [ ] The static site runs without a bundler and introduces no browser console errors.

## Verification Plan

- `git diff --check` — no whitespace errors.
- Run the local static server and the repository Playwright game client.
- Verify start, first-person render, top-down toggle, return to first-person, resize, and fullscreen.
- Capture and inspect a gameplay screenshot showing the straight, boundaries, and depth markers.
- Compare the screenshot with `window.render_game_to_text()` renderer and camera fields.
- Run `/work.review staged` before commit and push.

## Follow-ups

- [0002](0002-curved-elevated-track.md) adds the continuous curved, elevated course after this renderer foundation is pushed.
- [0003](0003-threejs-rider-steering.md) binds normalized steering and the rider cockpit after the course exists.

## Picked

- Picked at: 2026-07-13 22:35 Asia/Shanghai
- Owner: Codex `/work.loop`
- Execution: issue 0001 isolated worktree
- Notes: First dependency in the renderer migration sequence.
