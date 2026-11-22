---
title: KEXEP-0074
---

The parser came to a token that can't appear where it is. This is the
general parse error. The message names the token it found, and the caret
points at where it found it.

```kex
main do
  let x = 1 +
  IO.printLine(x)
end
```

```
example.kex:2:14: [KEXEP-0074]: Error, unexpected token: Newline
  |
2 |   let x = 1 +
  |              ^
```

Here the line ends right after `+`, so the parser is still waiting for the
other side of it.

The mistake is often just before the place the caret points at. Look for:

- an operator, comma or `=` with nothing after it
- an unclosed `(`, `[` or `{`, or an `end` too many or too few
- syntax from another language, such as `def` or `#{...}` in place of
  `${...}`

## Fixing it

Finish the expression:

```kex
main do
  let x = 1 + 2
  IO.printLine(x)
end
```

To split a long expression over lines, wrap it in parentheses. A line can't
end on an operator otherwise, and can't start with one either.
