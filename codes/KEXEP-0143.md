---
title: KEXEP-0143
---

The file ended before every block was closed. The `if` is missing its
`end`, so the last `end` closes the `if` and `main` is left open.

```kex
main do
  let n = 3
  if n > 2
    IO.printLine("big")
end
```

```
example.kex:5:4: [KEXEP-0143]: Error, expected 'end' to close main block, got Eof
  |
5 | end
  |    ^
```

The caret is at the end of the file, because that is where the parser
noticed. The missing `end` belongs further up, and the message says which
block is still open.

## Fixing it

```kex
main do
  let n = 3
  if n > 2
    IO.printLine("big")
  end
end
```
