📌 # tilt-rush: Publish the verified V1 and V2 static packages

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

- [ ] Remote source contains V1 `v1.0.4` and the final V2 commit.
- [ ] `mars-ladder-static/main` contains both verified packages and all referenced assets.
- [ ] The test sync workflow completes successfully.
- [ ] V1 and V2 explicit `index.html` URLs and V2 generated-asset URLs return HTTP 200.
- [ ] Test CDN page-level smoke checks report the expected version, no missing assets, and no browser errors.

## Verification

- Remote tag/commit comparison before and after push.
- GitHub Actions run status for the static test sync.
- `curl -I` against explicit V1/V2 entry files and generated assets.
- Playwright smoke checks against both test CDN URLs.
