---
title: KEXET-0434
---

`.or` takes a value, not a block. It never runs the block, so `count`
would be the block itself and not the `0` inside it.

```kex
main do
  let count = Integer.parse("4").or { 0 }
  IO.printLine(count)
end
```

```
example.kex:2:37: [KEXET-0434]: Error, `or` needs a fallback of type Integer, but got a block. `or` never calls it, so the block itself would be the answer; pass a plain default, or `match` on the result to compute one
  |
2 |   let count = Integer.parse("4").or { 0 }
  |                                     ^
```

For an optional, the same mistake is [KEXET-0433](../KEXET-0433/).

## Fixing it

Pass the value directly:

```kex
main do
  let count = Integer.parse("4").or(0)
  IO.printLine(count)
end
```

When the fallback takes work to compute, `match` on the result, and
compute it in the `Error` arm.
