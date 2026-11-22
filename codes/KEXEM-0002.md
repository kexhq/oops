---
title: KEXEM-0002
---

`Shapes` exports `Geometri`, and there is no module by that name. The one
in the file is spelled `Geometry`. Since nothing was exported,
`Shapes.Geometry` does not exist either, as [KEXET-0422](../KEXET-0422/).

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * r * r
end

module Shapes do
  export Geometri
end

main do
  IO.printLine(Shapes.Geometry.area(1.0))
end
```

```
example.kex:6:3: [KEXEM-0002]: Error, exported module not found: Geometri
  |
6 |   export Geometri
  |   ^^^^^^^^^^^^^^^
example.kex:10:31: [KEXET-0422]: Error, `Shapes` has no module `Geometry`
   |
10 |   IO.printLine(Shapes.Geometry.area(1.0))
   |                ^^^^^^^^^^^^^^^
```

## Fixing it

Spell the name the way the module declares it:

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * r * r
end

module Shapes do
  export Geometry
end

main do
  IO.printLine(Shapes.Geometry.area(1.0))
end
```

The exported module keeps its name under `Shapes`, so the call is
`Shapes.Geometry.area`.
