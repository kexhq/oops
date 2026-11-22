---
title: KEXEP-0124
---

`match` is a keyword, so a variable cannot be called that. The same goes
for `return`, `next`, `break`, `then`, `loop` and `when`, among others.

```kex
main do
  let match = 1
  IO.printLine(match)
end
```

```
example.kex:2:7: [KEXEP-0124]: Error, `match` is a reserved keyword in Kex, so it cannot name a variable. Rename it
  |
2 |   let match = 1
  |       ^^^^^
```

## Fixing it

Pick another name:

```kex
main do
  let found = 1
  IO.printLine(found)
end
```
