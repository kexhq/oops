---
title: KEXEP-0102
---

A `let` needs its value on the same line, after `=`. Kex has no
declaration without a value, so `let total: Integer` on its own is
incomplete.

```kex
main do
  let total: Integer
  IO.printLine(total)
end
```

```
example.kex:2:21: [KEXEP-0102]: Error, expected '=' in let binding, got Newline
  |
2 |   let total: Integer
  |                     ^
```

## Fixing it

Give it its value where you declare it:

```kex
main do
  let total: Integer = 0
  IO.printLine(total)
end
```

If the value is only known later, declare the `let` at that point, or use
a `var` and change it.
