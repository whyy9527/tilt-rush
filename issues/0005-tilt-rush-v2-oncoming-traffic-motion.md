📌 # tilt-rush: Make V2 traffic approach early and visibly

Created: 2026-07-17
Source: Player feedback that traffic still pops in and does not feel oncoming
Owner repo: `tilt-rush`
Depends on: [issue 0004](0004-tilt-rush-v2-default-difficulty.md)

## Goal

Make every traffic vehicle enter beyond the readable horizon and visibly close distance faster than the roadside scenery.

## Chosen Slice

Spawn traffic 72 world units ahead and advance its existing logical collision entity at 1.35 times rider travel speed, with the Three.js mesh continuing to render only from that logical entity.

## Scope

- Increase the shared traffic spawn distance from 44 to 72 world units.
- Increase the shared traffic visibility envelope to 90 world units.
- Apply one 1.35 oncoming approach multiplier to logical obstacle motion.
- Keep mesh position, collision, cleanup, timing telemetry, and screenshots bound to the same logical obstacle.

## Non-goals

- New vehicle models, traffic AI, lane changes, overtaking, or traffic physics.
- Difficulty profile, camera gestures, or environment art.

## Acceptance Criteria

- [ ] The first vehicle is rendered at least 70 world units ahead rather than appearing near the rider.
- [ ] At the default starting speed the first vehicle provides at least nine seconds before collision.
- [ ] Traffic closes distance 1.35 times faster than stationary roadside scenery.
- [ ] Steering, collision, jumping, cleanup, and Flow use the same visible logical vehicle with no invisible hit.

## Verification

- Deterministic distance and reaction-time assertions from `render_game_to_text()`.
- Separate steering, collision, jump, and cleanup scenarios.
- Far, mid, and close screenshots on desktop and 390x844 mobile.
- Browser-error check and `git diff --check`.
