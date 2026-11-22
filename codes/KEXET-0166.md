---
title: KEXET-0166
---

`square` is private to `Geometry`. `using Geometry` brings in the module's
public functions, here `area`, and leaves the private ones out.

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

using Geometry

main do
  IO.printLine(square(3.0))
end
```

```
example.kex:12:16: [KEXET-0166]: Error, undefined function: `square`. `Geometry.square` is private to `Geometry`
   |
12 |   IO.printLine(square(3.0))
   |                ^^^^^^^^^^^
```

Called as `Geometry.square`, the same mistake is
[KEXET-0426](../KEXET-0426/).

## Fixing it

Call a public function:

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

using Geometry

main do
  IO.printLine(area(3.0))
end
```

If `square` should be usable from outside, move it out of the
`private do ... end` block.
