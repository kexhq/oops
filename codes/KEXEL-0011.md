---
title: KEXEL-0011
---

`\x` followed by two hex digits is one byte, and in a string it may only
be an ASCII byte, `\x00` to `\x7f`. `é` is not ASCII. In UTF-8 it takes
two bytes, so `\xe9` alone would be half a character.

```kex
main do
  IO.printLine("caf\xe9")
end
```

```
example.kex:2:16: [KEXEL-0011]: Error, '\xe9' is not ASCII; write the character as '\u{e9}'
  |
2 |   IO.printLine("caf\xe9")
  |                ^^^^^^^^
```

## Fixing it

Write the character by its code point with `\u{...}`:

```kex
main do
  IO.printLine("caf\u{e9}")
end
```

You can also type `é` straight into the string: `"café"` is the same text.
