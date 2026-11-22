---
title: KEXET-0147
---

The code uses a name that isn't defined, and a defined name is spelled
almost the same. Usually it's a typo, and the message names the one you
probably meant.

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

With nothing close to suggest, the same mistake is
[KEXET-0146](../KEXET-0146/).

## Fixing it

Use the suggested name if it's the right one:

```kex
main do
  let total = 10
  IO.printLine(total)
end
```

If it isn't, you meant a new name. Define it first.
