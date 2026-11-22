---
title: KEXET-0442
---

A range runs between two values of the same type. `1` is an `Integer`,
and `limit` is a `Float`.

```kex
main do
  let limit = 5.0
  IO.printLine((1..limit).count)
end
```

```
example.kex:3:17: [KEXET-0442]: Error, range endpoints must have the same type
  |
3 |   IO.printLine((1..limit).count)
  |                ^^^^^^^^^^
```

## Fixing it

Make both ends `Integer`s:

```kex
main do
  let limit = 5
  IO.printLine((1..limit).count)
end
```
