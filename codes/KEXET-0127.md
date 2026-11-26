---
title: KEXET-0127
---

`half` says it returns an `Integer`, but `n / 2.0` is a `Float`. A
function's body returns the value of its last expression.

```kex
let half(n: Integer) -> Integer = n / 2.0

main do
  IO.printLine(half(5))
end
```

```
example.kex:1:39: [KEXET-0127]: Error, `half` declared to return Integer but body returns Float
  |
1 | let half(n: Integer) -> Integer = n / 2.0
  |                         -------   ^^^^^^^ this has type Float
  |                         |
  |                         expected because of this return type
```

A `return` of the wrong type is [KEXET-0124](../KEXET-0124/).

## Fixing it

If `half` should return a `Float`, change the signature:

```kex
let half(n: Integer) -> Float = n / 2.0

main do
  IO.printLine(half(5))
end
```

If it should return an `Integer`, write `n / 2`, which drops the remainder.
