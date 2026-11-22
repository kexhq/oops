---
title: KEXET-0165
---

`square` is defined in the `Geometry` module, but this code is outside it.
From outside, it has to be called through the module, or brought in with
`using`.

```kex
module Geometry do
  let square(n: Float) -> Float = n * n
end

main do
  IO.printLine(square(3.0))
end
```

```
example.kex:6:16: [KEXET-0165]: Error, undefined function: `square`. `Geometry.square` is not imported here
  |
6 |   IO.printLine(square(3.0))
  |                ^^^^^^^^^^^
```

## Fixing it

```kex
module Geometry do
  let square(n: Float) -> Float = n * n
end

main do
  IO.printLine(Geometry.square(3.0))
end
```

Or add `using Geometry` at the top of the code that calls it, and keep
calling it as `square`.
