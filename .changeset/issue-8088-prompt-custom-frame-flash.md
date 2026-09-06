---
"effect": patch
---

Buffer `Prompt.custom` clear and next-frame render so the previous frame stays visible while the next frame is being computed (#8088)

`runLoop` in `Prompt.ts` displayed the `clear` output as its own `display` call *before* the next frame was rendered. During a slow render this left a blank gap (flash) between the old and new frames. The clear output is now buffered and emitted together with the next frame's render in a single `display` call for both the `NextFrame` and `Submit` paths.
