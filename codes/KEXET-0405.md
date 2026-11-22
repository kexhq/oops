---
title: KEXET-0405
---

`map` wants a function, and `Just` on its own is a constructor, not a
function value. The message shows the block to write instead.

```kex
main do
  let scores = [3, 7]
  IO.printLine(scores.map(Just))
end
```

```
example.kex:3:27: [KEXET-0405]: Error, `Just` is a constructor taking 1 value, not a value: call it (`Just(…)`), or pass a block (`{ |x| Just(x) }`)
  |
3 |   IO.printLine(scores.map(Just))
  |                           ^^^^
```

## Fixing it

```kex
main do
  let scores = [3, 7]
  IO.printLine(scores.map { |n| Just(n) })
end
```
