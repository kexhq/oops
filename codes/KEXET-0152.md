---
title: KEXET-0152
---

`Dot` starts with a capital letter, so the compiler reads it as a
constructor or a type, and there is neither by that name. `Shape`'s
constructors are `Circle`, `Square` and `Point`.

```kex
type Shape = Circle(Float) | Square(Float) | Point

main do
  let shape = Dot
  IO.printLine(shape)
end
```

```
example.kex:4:15: [KEXET-0152]: Error, undefined constructor or type: `Dot`
  |
4 |   let shape = Dot
  |               ^^^
```

## Fixing it

Use one of the constructors the type has:

```kex
type Shape = Circle(Float) | Square(Float) | Point

main do
  let shape = Point
  IO.printLine(shape)
end
```

If `Dot` should exist, add it to the type: `type Shape = ... | Dot`.
