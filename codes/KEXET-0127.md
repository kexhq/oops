---
title: KEXET-0127
---

A function's body gives back a different type from the one its signature
declares. The value of the body is its last expression.

```kex
let half(n: Integer) -> Integer = n / 2.0

main do
  IO.printLine(half(5))
end
```

```
example.kex:1:1: [KEXET-0127]: Error, `half` declared to return Integer but body returns Float64
  |
1 | let half(n: Integer) -> Integer = n / 2.0
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

Dividing by `2.0` gives a `Float`. Dividing two `Integer`s, as in `n / 2`,
gives an `Integer` and drops the remainder.

An early `return` of the wrong type is [KEXET-0124](../KEXET-0124/).

## Fixing it

Change whichever side is wrong. Here the function should answer a `Float`:

```kex
let half(n: Integer) -> Float = n / 2.0

main do
  IO.printLine(half(5))
end
```

If it really should answer an `Integer`, write `n / 2` instead.
