---
title: KEXET-0114
---

`Rect` holds two values, and the pattern `Rect(side)` names only one. A
pattern has to name every value the constructor holds.

```kex
type Shape = Circle(Float) | Rect(Float, Float)

let area(shape: Shape) -> Float do
  match shape do
    Circle(r) => Math.PI * r * r
    Rect(side) => side * side
  end
end
```

```
example.kex:6:5: [KEXET-0114]: Error, `Rect` constructor takes 2 value(s), but the pattern destructures 1
  |
6 |     Rect(side) => side * side
  |     ^^^^^^^^^^
```

## Fixing it

Name both values:

```kex
type Shape = Circle(Float) | Rect(Float, Float)

let area(shape: Shape) -> Float do
  match shape do
    Circle(r) => Math.PI * r * r
    Rect(w, h) => w * h
  end
end

main do
  IO.printLine(area(Rect(2.0, 3.0)))
end
```

If you only need one of them, put `_` in place of the other, as in
`Rect(w, _)`.
