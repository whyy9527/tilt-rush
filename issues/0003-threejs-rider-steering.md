📌 # Bind normalized steering to the Three.js rider view

Created: 2026-07-13
Source: Split from [issue 0001](0001-threejs-first-person-renderer.md)
Owner repo: `tilt-rush`
Depends on: [issue 0002](0002-curved-elevated-track.md) completed and pushed

## Goal

Make the Three.js first-person slice keyboard-playable from start to finish by applying the existing normalized steering value to the rider line and cockpit lean without uncomfortable horizon roll.

## Context

Renderer and course geometry are separate prerequisites. This issue owns the rider-facing integration with the existing simulation and input boundary.

## Chosen Slice

Feed the existing normalized steering value into a course-relative lateral rider offset and a restrained cockpit lean while the camera stays aligned to the course horizon.

## Scope

- Position the first-person camera from the existing player lane relative to the Three.js course.
- Render a gray-box motorcycle cockpit that visibly leans with steering.
- Apply the current normalized keyboard or calibrated-camera steering value without changing its range or calibration.
- Keep camera roll restrained while preserving readable curve entry, crest, and landing motion.
- Preserve start, finish, restart, fullscreen, and view-toggle flows.
- Report rider course position, normalized steering, cockpit lean, and current course segment through `window.render_game_to_text()`.

## Non-goals

- Traffic, collisions, jump targets, scoring redesign, or top-down renderer migration.
- Webcam end-to-end validation or calibration changes.
- Final motorcycle model, city art, lighting polish, shake, or realistic simulation physics.

## Acceptance Criteria

- [ ] Left and right keyboard input move the rider line in opposite course-relative directions.
- [ ] The cockpit leans with normalized steering while horizon roll remains restrained.
- [ ] The renderer consumes the existing `[-1, 1]` steering value without changing webcam calibration behavior.
- [ ] Keyboard control can complete the course from start to finish and restart another run.
- [ ] Start, fullscreen, and first-person/top-down toggle flows remain usable.
- [ ] `window.render_game_to_text()` matches the visible rider line, steering, lean, course segment, and mode.
- [ ] The site remains deployable as static GitHub Pages content.

## Verification Plan

- `git diff --check` — no whitespace errors.
- Run the local static server and the repository Playwright game client.
- Verify start, sustained left/right steering, neutral recovery, course completion, restart, view toggle, and fullscreen.
- Capture and inspect gameplay screenshots on the straight, curve, and crest at neutral and steered positions.
- Compare screenshots with `window.render_game_to_text()` and confirm no new browser console errors.
- Run `/work.review staged` before commit and push.

## Why This Is Separate

Rider input and camera comfort can be verified only after the renderer and course geometry have stable world-space boundaries.

## Picked

- Picked at: 2026-07-13 22:51 Asia/Shanghai
- Owner: Codex `/work.loop`
- Execution: issue 0003 isolated worktree
- Notes: Issues 0001 and 0002 are completed and pushed; this is the final dependency in sequence.
