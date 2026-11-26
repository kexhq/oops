---
title: KEXET-0131
---

`Square` says it implements `Shape`, but its `make` block does not
define `area`, which every `Shape` must have.

```kex
trait Shape do
  area :> Float
end

record Square do
  side : Float
end

make Square, implement: Shape do
end
```

```
example.kex:9:1: [KEXET-0131]: Error, make Square, implement: Shape. Missing required function 'area'
  |
9 | make Square, implement: Shape do
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Define the missing function in the `make` block:

```kex
trait Shape do
  area :> Float
end

record Square do
  side : Float
end

make Square, implement: Shape do
  let area -> Float = @side * @side
end

main do
  IO.printLine(Square { side: 2.0 }.area)
end
```
