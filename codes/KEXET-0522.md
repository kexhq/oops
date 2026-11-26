---
title: KEXET-0522
---

`.as(List)` turns a tuple into a list when the compiler can see the
tuple's elements written out, as in `(1, 2).as(List)`. `p` comes from a
call, so the compiler knows its type but not its elements.

```kex
let point(x: Integer) -> (Integer, Integer) = (x, x * 2)

main do
  let p = point(3)
  IO.inspect(p.as(List))
end
```

```
example.kex:5:18: [KEXET-0522]: Error, `.as(List)` needs a tuple literal; for a tuple known only at run time use `.items`, or `.to(List)`
  |
5 |   IO.inspect(p.as(List))
  |              ^^^^^^^^^^
```

## Fixing it

Use `.items`, which works on any tuple:

```kex
let point(x: Integer) -> (Integer, Integer) = (x, x * 2)

main do
  let p = point(3)
  IO.inspect(p.items)
end
```

A tuple whose positions have different types gives a list of their union:
`(1, "x")` gives an `[Integer | String]`. `.to(List)` gives the same list
wrapped in an optional.
