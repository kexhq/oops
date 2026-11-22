---
title: KEXEM-0001
---

`export` passes another module's names on to whoever uses this one.
`Shapes` names itself, and that has no meaning: `area` is already one of
its own public names.

```kex
module Shapes do
  export Shapes

  let area(w: Float, h: Float) -> Float = w * h
end

main do
  IO.printLine(Shapes.area(2.0, 3.0))
end
```

```
example.kex:2:3: [KEXEM-0001]: Error, module cannot export itself
  |
2 |   export Shapes
  |   ^^^^^^^^^^^^^
```

## Fixing it

Delete the line. `Shapes.area` works without it:

```kex
module Shapes do
  let area(w: Float, h: Float) -> Float = w * h
end

main do
  IO.printLine(Shapes.area(2.0, 3.0))
end
```
