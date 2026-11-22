---
title: KEXET-0426
---

`square` is inside `private do ... end` in `Geometry`, so only the code in
`Geometry` can call it.

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

main do
  IO.printLine(Geometry.square(3.0))
end
```

```
example.kex:10:31: [KEXET-0426]: Error, cannot access private name `square` from Geometry
   |
10 |   IO.printLine(Geometry.square(3.0))
   |                ^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Call one of the public functions:

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

main do
  IO.printLine(Geometry.area(3.0))
end
```

If other code really needs `square`, move it out of the `private` block.
