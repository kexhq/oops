---
title: KEXEP-0074
---

The parser found a token that cannot go where it is. Here the line ends
after `+`, so there is nothing to add.

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

The same happens with an `=` that has nothing after it.

## Fixing it

```kex
main do
  let x = 1 + 2
  IO.printLine(x)
end
```

To split a long expression over several lines, put it in parentheses.
