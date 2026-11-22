---
title: KEXET-0147
---

`totl` is not defined, but `total` is, so the compiler guesses that is the
one you meant.

```kex
main do
  let total = 10
  IO.printLine(totl)
end
```

```
example.kex:3:16: [KEXET-0147]: Error, undefined name: `totl`, did you mean `total`?
  |
3 |   IO.printLine(totl)
  |                ^^^^
```

With no close match, the error is [KEXET-0146](../KEXET-0146/).

## Fixing it

```kex
main do
  let total = 10
  IO.printLine(total)
end
```

If the guess is wrong and `totl` is a new name, define it first.
