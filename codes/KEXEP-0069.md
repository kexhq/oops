---
title: KEXEP-0069
---

`${...}` holds one expression. `first last` is two names side by side,
which is not one expression.

```kex
main do
  let first = "Ada"
  let last = "Lovelace"
  IO.printLine("${first last}")
end
```

```
example.kex:4:16: [KEXEP-0069]: Error, interpolation must contain exactly one expression
  |
4 |   IO.printLine("${first last}")
  |                ^^^^^^^^^^^^^^^
```

## Fixing it

Give each value its own `${...}`, with the text between them outside:

```kex
main do
  let first = "Ada"
  let last = "Lovelace"
  IO.printLine("${first} ${last}")
end
```

To join a list of values, `[first, last].join(" ")` also works.
