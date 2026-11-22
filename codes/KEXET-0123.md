---
title: KEXET-0123
---

`A` and `B` are two type variables, so `pick` can be called with two
different types: `pick(1, "two")`. Then `b` is a `String`, while the
signature promises an `A`, which here is an `Integer`.

```kex
let pick(a: A, b: B) -> A = b
```

```
example.kex:1:1: [KEXET-0123]: Error, `pick` declared to return A but body returns `B`, which stands for any type
  |
1 | let pick(a: A, b: B) -> A = b
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

If both arguments always have the same type, use one letter for both:

```kex
let pick(a: A, b: A) -> A = b

main do
  IO.printLine(pick(1, 2))
end
```

If they can differ, say that `pick` returns the type of `b`: `-> B`.
