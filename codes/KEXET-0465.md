---
title: KEXET-0465
---

`*`, `-` and `/` work on numbers, not on text. In Ruby, `"-" * 10` repeats
the string; in Kex it is an error.

```kex
main do
  IO.printLine("-" * 10)
end
```

```
example.kex:2:22: [KEXET-0465]: Error, cannot use arithmetic operator on String
  |
2 |   IO.printLine("-" * 10)
  |                ^^^^^^^^
```

Adding a `String` and a number with `+` is
[KEXET-0463](../KEXET-0463/).

## Fixing it

```kex
main do
  IO.printLine("-".repeat(10))
end
```

If the string holds a number, convert it with `.to(Integer)` before doing
arithmetic on it.
