---
title: KEXET-0497
---

`-`, `*`, `/`, `%` and `^` work on numbers only. `done` is a `Bool`, which
has no arithmetic.

```kex
main do
  let done = true
  IO.printLine(done * 2)
end
```

```
example.kex:3:23: [KEXET-0497]: Error, operator '*' requires numbers, got Bool and Integer
  |
3 |   IO.printLine(done * 2)
  |                ^^^^^^^^
```

The same with a `String` is [KEXET-0465](../KEXET-0465/), and `+` between
two different types is [KEXET-0464](../KEXET-0464/).

## Fixing it

Use the number the value stands for:

```kex
main do
  let done = true
  let count = done then 1 else 0
  IO.printLine(count * 2)
end
```
