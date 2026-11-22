---
title: KEXEM-0007
---

`only:` lists names to import from `Geometry`, and `square` is private to
it. Private names cannot be imported, so the `using` line is rejected, and
the call to `square` fails as well, as
[KEXET-0166](../KEXET-0166/).

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

using Geometry, only: [square]

main do
  IO.printLine(square(3.0))
end
```

```
example.kex:9:1: [KEXEM-0007]: Error, cannot import private name `square` from Geometry
  |
9 | using Geometry, only: [square]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
example.kex:12:16: [KEXET-0166]: Error, undefined function: `square`. `Geometry.square` is private to `Geometry`
   |
12 |   IO.printLine(square(3.0))
   |                ^^^^^^^^^^^
```

## Fixing it

Import a public function:

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

using Geometry, only: [area]

main do
  IO.printLine(area(3.0))
end
```
