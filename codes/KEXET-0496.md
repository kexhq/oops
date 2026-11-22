---
title: KEXET-0496
---

The pattern on the left takes a tuple of two values apart, but the tuple on
the right has three. A pattern only matches a tuple of exactly its size.

```kex
main do
  let (name, age) = ("Ada", 36, "London")
  IO.printLine(name)
end
```

```
example.kex:2:7: [KEXET-0496]: Error, the tuple has 3 value(s), but the pattern destructures 2: `(String, Integer, String)`
  |
2 |   let (name, age) = ("Ada", 36, "London")
  |       ^^^^^^^^^^^
```

## Fixing it

Name every value, with `_` for the ones you do not need:

```kex
main do
  let (name, age, _) = ("Ada", 36, "London")
  IO.printLine(name)
end
```
