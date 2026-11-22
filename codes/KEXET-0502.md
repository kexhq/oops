---
title: KEXET-0502
---

`1.0..5.0` is a range of `Float`s: it has a start and an end, but no next
value after `1.0`, so there is nothing to count, map or sum.

```kex
main do
  IO.printLine((1.0..5.0).count)
end
```

```
example.kex:2:32: [KEXET-0502]: Error, `count` walks a range's values, and a Float range has none to walk: use an Integer range, or ask it `contains?`
  |
2 |   IO.printLine((1.0..5.0).count)
  |                ^^^^^^^^^^^^^^^^
```

## Fixing it

Walk an `Integer` range:

```kex
main do
  IO.printLine((1..5).count)
end
```

A `Float` range can still say whether it holds a value:

```kex
main do
  IO.printLine((1.0..5.0).contains?(2.5))
end
```
