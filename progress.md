Original prompt: 我们开始处理这个repo的issues，我非常兴奋，你加油，借用work-pre-loop和work-loop。记得要拆分issue，具体怎么拆分pre-loop里有写

## Progress

- 2026-07-13: Ran the work-pre-loop readiness pass on issue 0001.
- 2026-07-13: Split the renderer foundation, course geometry, and rider integration into issues 0001-0003 with explicit dependencies and verification plans.
- 2026-07-13: Readiness review selected separate WebGL and Canvas elements because a browser canvas cannot hold both WebGL and 2D contexts; view switching owns their visibility.
- 2026-07-13: Issue 0001 implementation added a pinned Three.js ESM import, dedicated WebGL renderer, perspective camera, static gray-box straight, boundaries, and depth markers.
- 2026-07-13: Playwright verified the first-person state and controls with no console errors. Canvas-only captures were intermittent for WebGL, so page screenshots were used to verify the rendered scene and top-down toggle without adding a production rendering workaround.
- 2026-07-13: Page-level browser checks passed first-person/top-down/first-person switching, 900x600 resize, fullscreen entry, renderer visibility, and text-state alignment.

## Next

- Issue 0001 implementation was pushed as `f06dbe1` and passed Playwright plus work-review gates.
- Execute issue 0002 through the work-loop implementation, Playwright verification, review, commit, and push gates.
- Continue with issue 0003 only after issue 0002 is completed and pushed.
