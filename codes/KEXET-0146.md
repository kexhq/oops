---
title: KEXET-0146
---

Nothing called `price` is in scope: no binding, parameter or function, and
nothing imported.

```kex
main do
  IO.printLine(price)
end
```

```
example.kex:2:16: [KEXET-0146]: Error, undefined name: `price`
  |
2 |   IO.printLine(price)
  |                ^^^^^
```

If a defined name is spelled close to it, you get
[KEXET-0147](../KEXET-0147/) instead, with that name as a suggestion.

## Fixing it

Define it before using it:

```kex
main do
  let price = 12
  IO.printLine(price)
end
```

If it lives in another module, import that module.
