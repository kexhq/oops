---
title: KEXET-0511
---

Some functions are defined for a generic type only when its type argument
can do something. A range is walked one value at a time, so `count`, `map`
and `sum` need the next value after each one: they work on `Range<A>` only
where `A` is `Discrete`. `Integer` and `Char` are, `Float` is not, since
there is no next `Float` after `1.0`.

```kex
main do
  IO.printLine((1.0..5.0).count)
end
```

```
example.kex:2:32: [KEXET-0511]: Error, `count` only works on Range<Float> when Float is Discrete, and Float isn't
  |
2 |   IO.printLine((1.0..5.0).count)
  |                ^^^^^^^^^^^^^^^^
```

## Fixing it

Use a type argument that meets the bound, here an `Integer` range:

```kex
main do
  IO.printLine((1..5).count)
end
```

Or keep to what the type offers without the bound: a `Float` range can
still say whether it holds a value.

```kex
main do
  IO.printLine((1.0..5.0).contains?(2.5))
end
```
