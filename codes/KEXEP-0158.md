---
title: KEXEP-0158
---

A block `if` has no `do`. The body starts on the next line, and `end`
closes it.

```kex
main do
  let n = 3
  if n > 2 do
    IO.printLine("big")
  end
end
```

```
example.kex:3:12: [KEXEP-0158]: Error, use 'then' instead of 'do' in if expression: `if cond then body end`
  |
3 |   if n > 2 do
  |            ^^
```

## Fixing it

```kex
main do
  let n = 3
  if n > 2
    IO.printLine("big")
  end
end
```

For a short `if` on one line, the message shows the other form:
`if n > 2 then IO.printLine("big") end`.
