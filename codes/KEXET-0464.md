---
title: KEXET-0464
---

`count` is an `Integer` and `extra` is a `Float`. `+` needs both sides to
have the same type.

```kex
main do
  let count: Integer = 3
  let extra: Float = 0.5
  IO.printLine(count + extra)
end
```

```
example.kex:4:24: [KEXET-0464]: Error, operator '+' requires matching types, got Integer and Float
  |
4 |   IO.printLine(count + extra)
  |                ^^^^^^^^^^^^^
```

## Fixing it

Convert the `Integer` first. `to(Float)` gives an optional, so `.or`
supplies a value for the case where it fails:

```kex
main do
  let count: Integer = 3
  let extra: Float = 0.5
  IO.printLine(count.to(Float).or(0.0) + extra)
end
```

If both should have been whole numbers, change the `Float` instead.
