🟡 # Replace the Canvas perspective renderer with Three.js

Created: 2026-07-13
Source: Engine decision following the first-person V1 evaluation

## Goal

Deliver a keyboard-playable Three.js first-person gray-box slice with one curved, elevated track while preserving the existing normalized steering contract.

## Context

The current first-person view projects top-down coordinates into a road-shaped polygon and draws a fixed cockpit overlay. This is sufficient to test controls, but it cannot produce convincing sight lines, elevation, corner entry, landing motion, or spatial traffic placement without growing a bespoke 3D renderer.

Three.js is the chosen rendering layer. The game remains a browser-native static deployment; this is not a separate V2 or a second game.

## Scope

- Introduce a Three.js scene and perspective camera in the existing game.
- Build one gray-box track containing a straight, a readable curve, and an elevation change.
- Render a first-person motorcycle cockpit, road boundaries, and enough roadside markers to communicate speed.
- Drive the new renderer from the existing normalized steering value and verify the slice with keyboard input.
- Preserve the current game shell, input boundary, and static GitHub Pages deployment.

## Non-goals

- Godot or Phaser migration.
- A second V2 entry point or repository.
- Final vehicle models, city art, lighting polish, or a complete campaign.
- Webcam end-to-end validation, traffic, collisions, jump feedback, scoring migration, or top-down camera migration.
- Multiplayer, accounts, backend services, or AirPods integration.
- Realistic motorcycle simulation physics.

## Acceptance Criteria

- [ ] The default view uses a Three.js `PerspectiveCamera` and no longer calls the Canvas pseudo-perspective renderer.
- [ ] One continuous course visibly curves and changes elevation in world space.
- [ ] Steering changes the motorcycle line and lean without rotating the horizon enough to make head control uncomfortable.
- [ ] The renderer consumes the existing normalized steering value without changing the webcam calibration contract.
- [ ] Keyboard control completes the gray-box course from start to finish.
- [ ] The game remains deployable as a static GitHub Pages site.

## Verification

- Run the local static server and the repository's Playwright game client.
- Verify start, keyboard steering, course completion, restart, and fullscreen flows.
- Capture and inspect gameplay screenshots for the straight, curve, and elevation change.
- Confirm `window.render_game_to_text()` reports the same view, player, track segment, and mode state visible on screen.
- Confirm the browser console contains no new errors and the GitHub Pages deployment succeeds.
