---
title: KEXET-0102
---

`Circle` was declared with one value, its radius, and it was given two.

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Circle(1.0, 2.0)
  IO.printLine(shape)
end
```

```
example.kex:4:15: [KEXET-0102]: Error, `Circle` takes 1 value, but got 2
  |
4 |   let shape = Circle(1.0, 2.0)
  |               ^^^^^^^^^^^^^^^^
```

A value of the wrong type is [KEXET-0104](../KEXET-0104/).

## Fixing it

Pass one value, `Circle(1.0)`. Here the two values were meant for a
rectangle:

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Rect(1.0, 2.0)
  IO.printLine(shape)
end
```
