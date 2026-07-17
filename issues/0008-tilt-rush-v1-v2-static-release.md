✅ # tilt-rush: Publish the verified V1 and V2 static packages

Created: 2026-07-17
Source: Player request to publish this V2 update and the V1 mobile-road fix unless already released
Owner repos: `tilt-rush`, `mars-ladder-static`
Depends on: issues 0004, 0005, 0006, and 0007 closed

## Goal

Publish the verified V1 mobile-road fix and completed V2 update to the existing MarsLadder static URLs.

## Chosen Slice

Push the V1 source fix as `v1.0.4`, push the V2 source update on `main`, copy each verified source package into its existing static version directory, and push one explicit `mars-ladder-static` release commit to trigger the test CDN workflow.

## Scope

- Confirm `v1.0.4` does not already exist remotely before tagging.
- Push the V1 fix commit and annotated `v1.0.4` tag.
- Push the verified V2 main commit.
- Copy V1 and V2 `index.html` plus their referenced local assets to `resources/games/tilt-rush/v1/` and `/v2/`.
- Push the static release commit and verify test CDN entry and new asset URLs return HTTP 200.

## Non-goals

- Student-route changes, new environment variables, production workflow dispatch, signed URLs, or cache-policy changes.
- Republishing an already-present V1 tag and identical static package.

## Acceptance Criteria

- [x] Remote source contains V1 `v1.0.4` and the final V2 commit.
- [x] `mars-ladder-static/main` contains both verified packages and all referenced assets.
- [x] The test sync workflow completes successfully.
- [x] V1 and V2 explicit `index.html` URLs and V2 generated-asset URLs return HTTP 200.
- [x] Test CDN page-level smoke checks report the expected version, no missing assets, and no browser errors.

## Verification

- Remote tag/commit comparison before and after push.
- GitHub Actions run status for the static test sync.
- `curl -I` against explicit V1/V2 entry files and generated assets.
- Playwright smoke checks against both test CDN URLs.

## Resolution

- Closed at: 2026-07-17 10:56 Asia/Shanghai
- Source releases: V1 `v1.0.4` at `ffbe63e`; V2 `main` at `a62735a`.
- Static release: `mars-ladder-static@a19d57b`.
- Test sync: GitHub Actions run `29550798491` completed successfully in 47 seconds.
- CDN verification:
  - V1 and V2 explicit `index.html` responses were HTTP 200 and byte-identical to the committed static packages.
  - The generated skybox, facade, and water-ground assets each returned HTTP 200.
  - Playwright loaded both versions at 390x844 with exact 390px scroll width, keyboard fallback, no failed requests, and no console/page errors.
  - V1 road drawing covered the complete mobile logical viewport.
  - V2 loaded all generated and traffic textures, rendered 98 buildings, and exposed two early oncoming cars at 60.6 and 69.6 world units with the 1.35 approach multiplier.
- Production workflow was not dispatched; this slice publishes to the existing test CDN only.
