---
title: KEXET-0104
---

`Circle` holds a `Float`, and `2` is an `Integer`.

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Circle(2)
  IO.printLine(shape)
end
```

```
example.kex:4:15: [KEXET-0104]: Error, `Circle` expects a value of type Float, but got Integer
  |
4 |   let shape = Circle(2)
  |               ^^^^^^^^^
```

The wrong number of values is [KEXET-0102](../KEXET-0102/).

## Fixing it

Write it as a `Float`:

```kex
type Shape = Circle(Float) | Rect(Float, Float)

main do
  let shape = Circle(2.0)
  IO.printLine(shape)
end
```
