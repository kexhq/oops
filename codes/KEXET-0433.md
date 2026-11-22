---
title: KEXET-0433
---

`.or` takes a value, not a block. It never runs the block, so the result
would be the block itself and not the `String` inside it.

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first.or { "nobody" })
end
```

```
example.kex:3:25: [KEXET-0433]: Error, `or` needs a fallback of type String, but got a block. `or` never calls it, so the block itself would be the answer; pass a plain default, or `match` on the optional to compute one
  |
3 |   IO.printLine(first.or { "nobody" })
  |                         ^
```

Wrapping the fallback in `Just` is [KEXET-0429](../KEXET-0429/).

## Fixing it

Pass the value directly:

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first.or("nobody"))
end
```

When the fallback takes work to compute, use a `match` on the optional
and compute it in the `None` arm.
