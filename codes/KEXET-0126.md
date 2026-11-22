---
title: KEXET-0126
---

`Shape` says `area` gives a `Float`. `Square` keeps its side as an
`Integer`, so `@side * @side` is an `Integer` too, and that is not what the
trait promised.

```kex
trait Shape do
  area :> Float
end

record Square do
  side : Integer
end

make Square, implement: Shape do
  let area = @side * @side
end
```

```
example.kex:10:3: [KEXET-0126]: Error, `area` is required to return Float but body returns Integer
   |
10 |   let area = @side * @side
   |   ^^^^^^^^^^^^^^^^^^^^^^^^
```

`area` has no `->` of its own, so it is held to the trait's `Float`. Code that
only knows it has a `Shape` will treat the answer as a `Float`.

## Fixing it

Make the body give a `Float`. Here the simplest way is to store the side as
one:

```kex
trait Shape do
  area :> Float
end

record Square do
  side : Float
end

make Square, implement: Shape do
  let area = @side * @side
end

main do
  IO.printLine(Square { side: 3.0 }.area)
end
```

If the trait is the one that is wrong, change `area :> Float` instead, and
every type that implements `Shape` with it.
