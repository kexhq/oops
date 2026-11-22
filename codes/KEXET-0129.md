---
title: KEXET-0129
---

Two modules here each have a trait called `Shape`, and neither is imported.
A bare `Shape` after `implement:` could be either one, so Kex will not pick.

```kex
module Geometry do
  trait Shape do
    area :> Float
  end
end

module Drawing do
  trait Shape do
    outline :> String
  end
end

record Square do
  side : Float
end

make Square, implement: Shape do
  let area = @side * @side
end
```

```
example.kex:17:1: [KEXET-0129]: Error, ambiguous trait: `Shape` could be `Drawing.Shape`, `Geometry.Shape`. Write the one you mean
   |
17 | make Square, implement: Shape do
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Name the module:

```kex
module Geometry do
  trait Shape do
    area :> Float
  end
end

module Drawing do
  trait Shape do
    outline :> String
  end
end

record Square do
  side : Float
end

make Square, implement: Geometry.Shape do
  let area = @side * @side
end

main do
  IO.printLine(Square { side: 2.0 }.area)
end
```

`using Geometry` above the `make` block also works, because then the bare
`Shape` is the one from `Geometry`.
