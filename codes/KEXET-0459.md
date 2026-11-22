---
title: KEXET-0459
---

`cond then a else b` has one type, so both sides must agree. Here one side
is a `String` and the other an `Integer`.

```kex
main do
  let n = 4
  let label = n > 0 then "positive" else 0
  IO.printLine(label)
end
```

```
example.kex:3:19: [KEXET-0459]: Error, branch type mismatch: 'then' returns String but 'else' returns Integer
  |
3 |   let label = n > 0 then "positive" else 0
  |               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

The same mistake in an `if ... else ... end` block is
[KEXET-0445](../KEXET-0445/).

## Fixing it

```kex
main do
  let n = 4
  let label = n > 0 then "positive" else "zero or less"
  IO.printLine(label)
end
```
