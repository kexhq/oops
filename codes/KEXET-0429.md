---
title: KEXET-0429
---

`.or` takes the value out of an optional, so its fallback has to be a plain
`String`. `Just("nobody")` is still an optional.

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first.or(Just("nobody")))
end
```

```
example.kex:3:25: [KEXET-0429]: Error, `or` needs a fallback of type String, but got `Just(…)`. `or` is what leaves the optional; pass a plain default, keep the value as it is, or `match` on it
  |
3 |   IO.printLine(first.or(Just("nobody")))
  |                         ^^^^^^^^^^^^^^
```

A block in place of the fallback is [KEXET-0433](../KEXET-0433/).

## Fixing it

Pass the plain value:

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first.or("nobody"))
end
```
