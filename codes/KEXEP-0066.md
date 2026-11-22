---
title: KEXEP-0066
---

A call was opened with `(` and never closed. The parser only notices when
it reaches something that cannot be an argument, here the `end` on the
next line, so the caret points there and not at the missing `)`.

```kex
main do
  IO.printLine((1 + 2)
end
```

```
example.kex:3:1: [KEXEP-0066]: Error, expected ')' after arguments, got end [end]
  |
3 | end
  | ^^^
```

## Fixing it

Count the brackets on the lines above the caret, and close the one that is
open:

```kex
main do
  IO.printLine((1 + 2))
end
```
