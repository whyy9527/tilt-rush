Original prompt: 我们开始处理这个repo的issues，我非常兴奋，你加油，借用work-pre-loop和work-loop。记得要拆分issue，具体怎么拆分pre-loop里有写

## Progress

- 2026-07-13: Ran the work-pre-loop readiness pass on issue 0001.
- 2026-07-13: Split the renderer foundation, course geometry, and rider integration into issues 0001-0003 with explicit dependencies and verification plans.
- 2026-07-13: Readiness review selected separate WebGL and Canvas elements because a browser canvas cannot hold both WebGL and 2D contexts; view switching owns their visibility.
- 2026-07-13: Issue 0001 implementation added a pinned Three.js ESM import, dedicated WebGL renderer, perspective camera, static gray-box straight, boundaries, and depth markers.
- 2026-07-13: Playwright verified the first-person state and controls with no console errors. Canvas-only captures were intermittent for WebGL, so page screenshots were used to verify the rendered scene and top-down toggle without adding a production rendering workaround.
- 2026-07-13: Page-level browser checks passed first-person/top-down/first-person switching, 900x600 resize, fullscreen entry, renderer visibility, and text-state alignment.
- 2026-07-13: Issue 0002 implementation replaced the flat plane with one generated centerline course, aligned road boundaries/lane markers/roadside posts to it, and bound the camera plus text state to existing total distance.
- 2026-07-13: Browser verification reached straight, curve, climb, crest, and descent with three lives intact; screenshots showed continuous road/edge/marker geometry and matching course telemetry, and top-down remained usable with no console errors.
- 2026-07-13: Issue 0003 implementation bound existing normalized steering to course-relative camera position and a camera-mounted gray-box cockpit, kept horizon roll at zero, mapped jump height into restrained camera lift, and added final-course completion.
- 2026-07-13: Browser flow verified opposite left/right lateral extremes and cockpit lean, neutral lean recovery, jump lift, top-down toggle, full course completion with three lives, and restart; the run exposed and fixed stale jump height on immediate restart.
- 2026-07-13: Final visual checks covered a steered curve and neutral crest, text state matched the visible lateral/lean/segment state, fullscreen entered and exited through both button and keyboard flows, and the console stayed error-free.
- 2026-07-14: Version split work began from the user decision that the completed top-down game is V1 and all first-person work is V2.
- 2026-07-14: Historical review found no pure top-down commit; the first public commit `306d8af` already mixed Canvas top-down and first-person renderers.
- 2026-07-14: Derived the V1 candidate from `306d8af`, removed the first-person renderer and view switching, retained camera/keyboard input and the completed gameplay, and isolated local best score under `tilt-rush-v1-best`.
- 2026-07-14: The required web-game Playwright client verified start, left/right steering, jump, and fixed V1/top-down text state; page-level checks confirmed one visible Canvas and no view button or console errors.
- 2026-07-14: A simulated camera permission denial produced `Camera denied · keyboard mode`, after which keyboard steering still advanced the run; menu and gameplay screenshots were visually inspected.
- 2026-07-14: The first work-review pass caught that the historical visual baseline predated the later final-course completion and restart jump reset; both completed-simulation behaviors were restored before submission.
- 2026-07-14: The post-fix browser run completed all four stages with the fixed top-down renderer, stored the V1 best score only under `tilt-rush-v1-best`, displayed the course-complete menu, and restarted with zero jump height.
- 2026-07-14: V1 was pushed and tagged `v1.0.0`; V2 work restored the reviewed `cfb7bc0` Three.js baseline after that tag and removed the hidden top-down canvas, top-down draw functions, and view switching without changing the shared simulation.
- 2026-07-14: Playwright verified the V2 menu, single WebGL canvas, fixed `v2` / `three` / `first-person` state, right/left steering, jump, inert `V` key, camera-denied keyboard fallback, all four stages, course completion, restart, and V2-only best-score storage with no console errors.
- 2026-07-14: Menu, active Three.js gameplay, camera-denied gameplay, and course-complete screenshots were visually inspected.
- 2026-07-15: New work split into workspace issues 0007 (automatic V1/V2 camera startup) and 0008 (visible V2 traffic); inspection confirmed V2 logical obstacles spawn and collide but have no Three.js scene object, which is the direct cause of invisible damage.
- 2026-07-15: V2 now calls its existing camera enable/calibration flow once at page boot; the manual toggle and keyboard fallback remain unchanged.
- 2026-07-15: V2 traffic now creates lightweight Three.js vehicles, maps logical approach distance and lane identity onto the course, synchronizes them before render, removes scene objects with logical obstacles, and exposes distance/rendered state for deterministic tests.
- 2026-07-15: Granted-camera testing found the automatic calibration overlay blocked the external disable button; V1 and V2 now provide an in-dialog `Use keyboard instead` action that reuses the normal camera shutdown path.
- 2026-07-15: Instrumented Playwright verified one automatic camera request in each version, denied-camera keyboard steering, granted-camera calibration entry and in-dialog shutdown, visible V2 traffic at 16.2 world units before collision, one-life collision loss, jump clear, game-over restart cleanup, and full four-stage completion with three lives.
- 2026-07-15: Work-review removed renderer ownership from logical obstacles by moving mesh identity into a renderer-owned Map, corrected V1 tag documentation, and strengthened granted-camera verification to require calibration state.
- 2026-07-15: V1 camera startup shipped as `v1.0.1` at `75215db`; V2 camera startup and visible traffic shipped on `main` at `c2eefc9`, and GitHub Pages run `29382531736` passed.
- 2026-07-15: The exact reviewed V1/V2 HTML packages were published through `mars-ladder-static@67c4bbb`; workflow `29382623463` passed, both explicit test CDN URLs returned HTTP 200, and CDN SHA-256 values matched source.
- 2026-07-15: Deployment QA at `marsladder-ai-qa@5be88ed` passed all three V1 static, V2 static, and student-route tests. Both versions requested camera once automatically and retained keyboard fallback; V2 exposed two rendered traffic meshes before collision range; desktop/mobile routes retained navigation with zero horizontal overflow.
- 2026-07-15: Workspace issues 0007 and 0008 reached terminal done state with source, static release, workflow, and deployed QA evidence.
- 2026-07-15: Issue 0010 isolated the shared mobile camera failure to preview playback after stream acquisition: both game packages had `playsinline muted` and the student iframe already delegated `camera` plus `autoplay`, but the preview omitted declarative autoplay and treated a mobile `video.play()` policy rejection as a fatal camera error.
- 2026-07-15: V1 and V2 now set autoplay/muted/inline playback before attaching the stream and retain the granted stream behind an in-dialog `Start camera` recovery action when the browser requires one tap.
- 2026-07-15: Mobile Chromium and WebKit verification passed automatic playback and one-tap recovery for both versions: each path requested camera once, recovery retried only video playback, and `Use keyboard instead` stopped the retained track. Standard game checks, granted/denied camera paths, visible V2 traffic, collision/jump cleanup, restart, and four-stage completion also passed.
- 2026-07-15: The mobile fix shipped as V1 tag `v1.0.2` at `6dab99e` and V2 `main` at `8ec6daf`; GitHub Pages run `29426288198` passed.
- 2026-07-15: Exact V1/V2 packages shipped through `mars-ladder-static@9013dcc`; GitGuardian `29426327394` and test sync `29426327452` passed, both CDN entries returned HTTP 200, and deployed hashes matched source.
- 2026-07-15: Deployment QA at `marsladder-ai-qa@3e32c79` passed V1 static, V2 static, and student-route cases. Both cross-origin student iframes delegated autoplay/camera and recovered a blocked first video playback with request/play counts `1/2`, while preserving keyboard fallback, navigation, and track cleanup.
- 2026-07-15: Workspace issue 0010 reached terminal done state with source, tag, static release, workflows, mobile-browser matrix, and deployed QA evidence.

## Next

- Issue 0001 implementation was pushed as `f06dbe1` and passed Playwright plus work-review gates.
- Issue 0002 implementation was pushed as `794ac2b` and passed segmented Playwright plus work-review gates.
- Issue 0003 implementation was pushed as `f94cfaf` and passed full rider-flow Playwright plus work-review gates.
- Return to the first-person design discussion from the mobile-camera-compatible V2 baseline.
