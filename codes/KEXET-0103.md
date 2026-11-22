---
title: KEXET-0103
---

`Rect` was declared with two values, a width and a height, and it was
given one.

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Rect(2.0)
  IO.printLine(shape)
end
```

```
example.kex:4:15: [KEXET-0103]: Error, `Rect` takes 2 values, but got 1
  |
4 |   let shape = Rect(2.0)
  |               ^^^^^^^^^
```

One value too many or too few for a constructor that takes one, such as
`Circle`, is [KEXET-0102](../KEXET-0102/).

## Fixing it

Pass both values. For a square, the width and height are the same:

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Rect(2.0, 2.0)
  IO.printLine(shape)
end
```
