✅ # tilt-rush: Make the V2 default run more forgiving

Created: 2026-07-17
Source: Player feedback that the current V2 run is still too difficult
Owner repo: `tilt-rush`

## Goal

Let a first-time player read traffic and finish substantially more of the course without adding a difficulty-selection UI.

## Chosen Slice

Tune the existing single V2 ruleset to start slower, accelerate more gently, cap at a lower speed, and provide four lives.

## Scope

- Replace duplicated speed and life literals with one default gameplay profile.
- Start at 220 km/h, accelerate by 7 km/h per second, and cap at 460 km/h.
- Start and restart with four lives while preserving collision, score, Flow, stage, and completion rules.
- Keep the existing three-lane course and stage patterns.

## Non-goals

- Difficulty selection, settings persistence, adaptive difficulty, or per-player tuning.
- Traffic appearance, spawn distance, camera gestures, or environment art.

## Acceptance Criteria

- [x] A new and restarted run begins at 220 km/h with four lives.
- [x] Speed never exceeds 460 km/h and grows at 7 km/h per second while playing.
- [x] One unprotected collision removes exactly one life.
- [x] Existing scoring, Flow, stages, completion, and restart remain functional.

## Verification

- Deterministic Playwright state checks at start, after acceleration, collision, completion, and restart.
- Standard web-game client screenshot and browser-error check.
- `git diff --check`.

## Resolution

- Closed at: 2026-07-17 09:14 Asia/Shanghai
- Commit: `5ce2126`
- Verification:
  - Standard web-game client — passed gameplay screenshot, text-state, and browser-error checks.
  - Deterministic Playwright state flow — passed 220 km/h profile, seven-per-second acceleration, four lives, one-life collision, and clean restart.
  - `git diff --check` — passed.
- Notes: The one default ruleset is more forgiving without adding settings or alternate modes.
