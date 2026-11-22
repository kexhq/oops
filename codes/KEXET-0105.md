---
title: KEXET-0105
---

The second value of `Rect` is a `Float`, and `3` is an `Integer`. The
message counts the values from 1.

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Rect(2.0, 3)
  IO.printLine(shape)
end
```

```
example.kex:4:15: [KEXET-0105]: Error, `Rect` expects value 2 of type Float, but got Integer
  |
4 |   let shape = Rect(2.0, 3)
  |               ^^^^^^^^^^^^
```

For a constructor with only one value, the same mistake is
[KEXET-0104](../KEXET-0104/).

## Fixing it

Write it as a `Float`:

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Rect(2.0, 3.0)
  IO.printLine(shape)
end
```
