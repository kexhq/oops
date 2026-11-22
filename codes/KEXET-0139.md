---
title: KEXET-0139
---

`Circle` and `Square` belong to `Shapes`, and `describe` is outside that
module. Each arm that names one without the module gets its own error.

```kex
module Shapes do
  type Shape = Circle(Float) | Square(Float)
end

let describe(shape: Shapes.Shape) -> String do
  match shape do
    Circle(r) => "circle of ${r}"
    Square(side) => "square of ${side}"
  end
end
```

```
example.kex:7:5: [KEXET-0139]: Error, `Circle` is `Shapes.Circle` here: name it so, or bring it in with `using Shapes`
  |
7 |     Circle(r) => "circle of ${r}"
  |     ^^^^^^^^^
example.kex:8:5: [KEXET-0139]: Error, `Square` is `Shapes.Square` here: name it so, or bring it in with `using Shapes`
  |
8 |     Square(side) => "square of ${side}"
  |     ^^^^^^^^^^^^
```

A constructor from a standard library module, such as `Append` from `FS`,
gives [KEXET-0138](../KEXET-0138/) instead.

## Fixing it

Name them with the module:

```kex
module Shapes do
  type Shape = Circle(Float) | Square(Float)
end

let describe(shape: Shapes.Shape) -> String do
  match shape do
    Shapes.Circle(r) => "circle of ${r}"
    Shapes.Square(side) => "square of ${side}"
  end
end

main do
  IO.printLine(describe(Shapes.Circle(1.0)))
end
```

Or add `using Shapes` before `describe`. Then `Circle`, `Square` and the
type `Shape` can all be written without `Shapes.` in front.
