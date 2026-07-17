📌 # tilt-rush: Replace the V2 gray-box world with generated environment art

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

- [ ] Generated sky, facade, and ground assets exist in the repository and are loaded by V2.
- [ ] The camera never reveals a flat clear-color void; the skybox remains visible through all stages.
- [ ] Textured building silhouettes surround the road without entering the five-unit road half-width.
- [ ] Ground imagery covers the complete 370-world-unit course.
- [ ] Straight, Dockside, Neon, Skyway, completion, restart, and 390x844 screenshots show a coherent finished environment with no browser errors.

## Verification

- Texture-load and environment-count telemetry assertions.
- Stage checkpoint screenshots plus completion/restart checks.
- Road-clearance checks for every generated building anchor.
- Standard web-game client and `git diff --check`.
