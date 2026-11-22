---
title: KEXET-0115
---

`Shape` has only `Circle` and `Square`. There is no `Triangle`, so that arm
could never match.

```kex
type Shape = Circle(Float) | Square(Float)

let area(shape: Shape) -> Float do
  match shape do
    Circle(r) => Math.PI * r * r
    Square(side) => side * side
    Triangle(base, height) => base * height / 2.0
  end
end
```

```
example.kex:7:5: [KEXET-0115]: Error, `Triangle` is not a constructor of `Shape` (it has `Circle`, `Square`). This pattern can never match
  |
7 |     Triangle(base, height) => base * height / 2.0
  |     ^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

If shapes can be triangles, add the constructor to the type:

```kex
type Shape = Circle(Float) | Square(Float) | Triangle(Float, Float)

let area(shape: Shape) -> Float do
  match shape do
    Circle(r) => Math.PI * r * r
    Square(side) => side * side
    Triangle(base, height) => base * height / 2.0
  end
end

main do
  IO.printLine(area(Triangle(2.0, 3.0)))
end
```

If the arm is left over from an older version of the type, delete it.
