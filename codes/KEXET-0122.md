---
title: KEXET-0122
---

`Shape` declares `scale :> Float -> This`, so whoever calls `scale` on a
`Shape` passes it a `Float`. `Square` wrote its `scale` to take an
`Integer`.

```kex
trait Shape do
  area :> Float
  scale :> Float -> This
end

record Square do
  side : Float
end

make Square, implement: Shape do
  let area = @side * @side
  let scale(by: Integer) = New { side: @side * by }
end
```

```
example.kex:12:17: [KEXET-0122]: Error, `scale` is required to take Float for `by`, but takes Integer
   |
12 |   let scale(by: Integer) = New { side: @side * by }
   |                 ^^^^^^^
```

## Fixing it

Take what the trait passes:

```kex
trait Shape do
  area :> Float
  scale :> Float -> This
end

record Square do
  side : Float
end

make Square, implement: Shape do
  let area = @side * @side
  let scale(by: Float) = New { side: @side * by }
end

main do
  IO.printLine(Square { side: 2.0 }.scale(3.0).area)
end
```
