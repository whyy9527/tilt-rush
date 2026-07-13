📌 # Build one curved, elevated Three.js course

Created: 2026-07-13
Source: Split from [issue 0001](0001-threejs-first-person-renderer.md)
Owner repo: `tilt-rush`
Depends on: [issue 0001](0001-threejs-first-person-renderer.md) completed and pushed

## Goal

Render one continuous Three.js gray-box course whose centerline visibly curves and changes elevation as existing game distance advances.

## Context

The renderer foundation deliberately contains only a static straight. This issue owns course geometry and progress binding, not rider controls or gameplay-system migration.

## Chosen Slice

Use one deterministic centerline to generate the road surface, boundaries, and roadside markers, then move the first-person camera forward along that course from existing distance state.

## Scope

- Define one finite course centerline with a straight, readable curve, crest, and descent.
- Generate a continuous road surface and boundaries from that centerline.
- Place repeated roadside markers that make forward speed and elevation readable.
- Bind camera course progress to existing distance state without changing game rules.
- Report the visible course segment and world-space elevation through `window.render_game_to_text()`.

## Non-goals

- Rider lateral steering, cockpit, camera lean, traffic, collision, or jump rendering.
- Multiple tracks, procedural generation, editor tooling, final art, or realistic physics.
- Changes to scoring, levels, webcam calibration, or keyboard input.

## Acceptance Criteria

- [ ] One continuous road contains a straight, a visible curve, an elevated crest, and a descent.
- [ ] Forward distance moves the camera continuously along the course without visible geometry seams.
- [ ] Road boundaries and roadside markers remain aligned through the curve and elevation change.
- [ ] `window.render_game_to_text()` reports the visible course segment, progress, and elevation.
- [ ] Existing top-down mode and normalized input state remain unchanged.

## Verification Plan

- `git diff --check` — no whitespace errors.
- Run the local static server and the repository Playwright game client.
- Capture and inspect screenshots at the straight, curve, crest, and descent.
- Compare each screenshot with the course segment, progress, and elevation in `window.render_game_to_text()`.
- Verify top-down toggle still works and the browser console has no new errors.
- Run `/work.review staged` before commit and push.

## Why This Is Separate

Course generation has a geometry-and-progress verification path independent from renderer initialization and rider steering.

## Picked

- Picked at: 2026-07-13 22:42 Asia/Shanghai
- Owner: Codex `/work.loop`
- Execution: issue 0002 isolated worktree
- Notes: Issue 0001 is completed and pushed; this is the next dependency in sequence.
