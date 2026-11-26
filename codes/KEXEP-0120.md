---
title: KEXEP-0120
---

`&:upperCase` is Ruby. In Kex the shorthand for "call this function on each
element" is `&.upperCase`, with a dot.

```kex
main do
  IO.printLine(["ada", "alan"].map(&:upperCase))
end
```

```
example.kex:2:37: [KEXEP-0120]: Error, expected '.' after '&': '&' is receiver shorthand, as in `&.size`
  |
2 |   IO.printLine(["ada", "alan"].map(&:upperCase))
  |                                     ^^^^^^^^^^
```

## Fixing it

```kex
main do
  IO.printLine(["ada", "alan"].map(&.upperCase))
end
```

`&.upperCase` is short for `{ |name| name.upperCase }`.
