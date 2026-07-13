Original prompt: 我们开始处理这个repo的issues，我非常兴奋，你加油，借用work-pre-loop和work-loop。记得要拆分issue，具体怎么拆分pre-loop里有写

## Progress

- 2026-07-13: Ran the work-pre-loop readiness pass on issue 0001.
- 2026-07-13: Split the renderer foundation, course geometry, and rider integration into issues 0001-0003 with explicit dependencies and verification plans.
- 2026-07-13: Readiness review selected separate WebGL and Canvas elements because a browser canvas cannot hold both WebGL and 2D contexts; view switching owns their visibility.

## Next

- Execute issue 0001 through the work-loop implementation, Playwright verification, review, commit, and push gates.
- Continue with issues 0002 and 0003 only after their dependencies are completed and pushed.
