---
title: KEXEL-0017
---

The string that starts at the caret is never closed. The `"` after `hello`
is missing, so the `)` became part of the string.

```kex
main do
  IO.printLine("hello)
end
```

```
example.kex:2:16: [KEXEL-0017]: Error, unterminated string
  |
2 |   IO.printLine("hello)
  |                ^^^^^^^
```

## Fixing it

```kex
main do
  IO.printLine("hello")
end
```
