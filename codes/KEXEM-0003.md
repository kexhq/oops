---
title: KEXEM-0003
---

`only:` asks for `circleArea`, and `Geometry` has no name like that. Its
function is called `area`. The call to `circleArea` then fails too, as
[KEXET-0163](../KEXET-0163/).

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * r * r
end

using Geometry, only: [circleArea]

main do
  IO.printLine(circleArea(3.0))
end
```

```
example.kex:5:1: [KEXEM-0003]: Error, module Geometry has no name `circleArea`
  |
5 | using Geometry, only: [circleArea]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
example.kex:8:16: [KEXET-0163]: Error, undefined function: `circleArea`
  |
8 |   IO.printLine(circleArea(3.0))
  |                ^^^^^^^^^^^^^^^
```

## Fixing it

List names the module has:

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * r * r
end

using Geometry, only: [area]

main do
  IO.printLine(area(3.0))
end
```
