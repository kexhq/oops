---
title: KEXET-0146
---

The code uses a name that nothing in scope defines: no `let` or `var`
before it, no parameter, no function and no import.

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

When a defined name is close in spelling, you get
[KEXET-0147](../KEXET-0147/) instead, which suggests it.

## Fixing it

Define the name before you use it:

```kex
main do
  let price = 12
  IO.printLine(price)
end
```

If you thought it was defined, check the spelling and whether it's defined
in another file you haven't imported.
