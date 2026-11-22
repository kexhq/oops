---
title: KEXEL-0019
---

Single quotes hold exactly one character, a `Char`. `'hello'` has five, so
the character literal ends where the second one should be a closing `'`.

```kex
main do
  IO.printLine('hello')
end
```

```
example.kex:2:16: [KEXEL-0019]: Error, unterminated char literal
  |
2 |   IO.printLine('hello')
  |                ^^
```

## Fixing it

Text goes in double quotes:

```kex
main do
  IO.printLine("hello")
end
```
