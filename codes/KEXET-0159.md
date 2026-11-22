---
title: KEXET-0159
---

`totl` is not a variable, but `total` is. It is a typo, and the compiler
suggests the variable you meant.

```kex
main do
  var total = 0
  totl = 10
  IO.printLine(total)
end
```

```
example.kex:3:3: [KEXET-0159]: Error, undefined variable: `totl`, did you mean `total`?
  |
3 |   totl = 10
  |   ^^^^^^^^^
```

Without a close match, the error is [KEXET-0158](../KEXET-0158/).

## Fixing it

```kex
main do
  var total = 0
  total = 10
  IO.printLine(total)
end
```
