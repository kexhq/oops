---
title: KEXET-0466
---

`18 <= age < 65` is read as `(18 <= age) < 65`. The first comparison
gives a `Bool`, and a `Bool` cannot be compared with `<`.

```kex
main do
  let age = 30
  IO.printLine(18 <= age < 65)
end
```

```
example.kex:3:28: [KEXET-0466]: Error, cannot compare Bool values with '<', '>', '<=', '>='
  |
3 |   IO.printLine(18 <= age < 65)
  |                ^^^^^^^^^^^^^^
```

## Fixing it

Write two comparisons, joined with `&&`:

```kex
main do
  let age = 30
  IO.printLine(18 <= age && age < 65)
end
```
