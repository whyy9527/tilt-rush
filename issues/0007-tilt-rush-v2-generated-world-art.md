✅ # tilt-rush: Replace the V2 gray-box world with generated environment art

Created: 2026-07-17
Source: Player request for a complete map scene, finished roadside buildings, and an essential skybox using image generation
Owner repo: `tilt-rush`

## Goal

Give the complete V2 course a coherent finished night-city world instead of flat fog and untextured blockout structures.

## Chosen Slice

Generate one equirectangular night-city skybox and one futuristic building-facade texture, derive a seamless city-water ground texture from the generated skybox water, and map all three assets onto the existing Three.js course and reusable low-poly environment geometry.

## Scope

- Generate the skybox and facade texture with the built-in image generation tool, then derive the seamless water ground from the generated skybox without introducing an older or non-generated source.
- Save versioned final assets under `assets/environment/`.
- Render the skybox as scene background/environment imagery rather than a flat color.
- Add textured roadside building masses outside the road envelope across all four stages.
- Apply the generated ground texture around the full course while preserving the wet-asphalt road.
- Reuse shared geometry, textures, and instancing where possible.

## Non-goals

- A level editor, downloadable 3D models, photogrammetry, dynamic weather, interiors, or a second course.
- Changes to collision, score, traffic, input, or stage progression.

## Acceptance Criteria

- [x] Generated sky, facade, and ground assets exist in the repository and are loaded by V2.
- [x] The camera never reveals a flat clear-color void; the skybox remains visible through all stages.
- [x] Textured building silhouettes surround the road without entering the five-unit road half-width.
- [x] Ground imagery covers the complete 370-world-unit course.
- [x] Straight, Dockside, Neon, Skyway, completion, restart, and 390x844 screenshots show a coherent finished environment with no browser errors.

## Verification

- Texture-load and environment-count telemetry assertions.
- Stage checkpoint screenshots plus completion/restart checks.
- Road-clearance checks for every generated building anchor.
- Standard web-game client and `git diff --check`.

## Resolution

- Closed at: 2026-07-17 10:39 Asia/Shanghai
- Commit: `42f579f`
- Verification:
  - Built-in Image 2 outputs — inspected the 1774x887 skybox and 1254x1254 facade; inspected the final 1024x1024 seamless water derivative from the generated skybox.
  - Standard web-game client — passed all three texture loads, 98-building inventory, 69-unit traffic readability, screenshot, and browser-error checks.
  - Four-stage automated drive — passed Stage 1, Dockside, Neon, Skyway, completion with real collisions enabled, and restart without duplicating environment instances.
  - Desktop and 390x844 Skyway runs — passed all texture loads, at least one remaining life, exact viewport scroll width, and no browser errors.
  - Visual review — inspected generated assets plus Stage 1, Dockside, Neon, Skyway, completion, jump, traffic, and mobile screenshots.
  - `git diff --check` — passed.
- Notes: The image service rejected three separate ground-only generations at its network layer. The shipped ground is therefore a seamless local derivative of the successfully generated skybox water, keeping every new world pixel sourced from this run's Image 2 output without switching models.
