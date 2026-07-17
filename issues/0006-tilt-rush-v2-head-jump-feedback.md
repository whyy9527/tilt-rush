✅ # tilt-rush: Make the V2 upward-head jump obvious

Created: 2026-07-17
Source: Player feedback that lifting the head does not clearly trigger or show a jump
Owner repo: `tilt-rush`

## Goal

Make a deliberate upward head flick trigger reliably and produce an unmistakable first-person lift without allowing downward motion to trigger it.

## Chosen Slice

Detect only a negative calibrated pitch delta at a lower threshold, then amplify the existing camera/cockpit jump animation and show a short `JUMP` HUD pulse from the existing jump state.

## Scope

- Replace the absolute pitch-delta trigger with an upward-only `-0.065` threshold.
- Keep the existing jump cooldown and collision-clear rules.
- Increase first-person camera lift and add a short cockpit dip/recovery.
- Render a non-interactive `JUMP` pulse while `jumpPulse` is active.
- Expose the threshold and pulse in text telemetry.

## Non-goals

- A new pose model, gesture-training flow, camera upload, or keyboard-control change.
- Difficulty, traffic motion, or environment art.

## Acceptance Criteria

- [x] An upward pitch delta beyond the threshold triggers one jump when cooldown permits.
- [x] Equal downward pitch movement does not trigger a jump.
- [x] The first-person camera lift, cockpit motion, and `JUMP` pulse are visibly present during the jump.
- [x] Space still triggers the same jump and one jump can clear one visible vehicle without damage.

## Verification

- Deterministic gesture-threshold checks through a test hook that calls the production gesture decision.
- Keyboard jump and traffic-clear state checks.
- Jump apex screenshot on desktop and mobile.
- Browser-error check and `git diff --check`.

## Resolution

- Closed at: 2026-07-17 09:28 Asia/Shanghai
- Commit: `2a34f4f`
- Verification:
  - Production gesture decision — passed at and beyond `-0.065`; smaller upward movement and positive/downward movement did not trigger.
  - Standard web-game client — passed active `JUMP` feedback, 52-unit lift screenshot, telemetry, and browser-error checks.
  - Desktop and 390x844 distance-triggered jump flows — passed 80.6-unit apex, visible cockpit/feedback motion, one jump, one clear, and four lives retained.
  - `git diff --check` — passed.
- Notes: Both camera and Space input still feed the same jump function; only the camera gesture decision and presentation changed.
