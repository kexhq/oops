---
title: KEXEP-0063
---

`cond then a else b` is an expression, and it has to have a value either
way. Without the `else`, there would be nothing for `size` to be when
`n > 3` is false.

```kex
main do
  let n = 4
  let size = n > 3 then "big"
  IO.printLine(size)
end
```

```
example.kex:3:30: [KEXEP-0063]: Error, expected 'else' after 'then', got Newline
  |
3 |   let size = n > 3 then "big"
  |                              ^
```

## Fixing it

```kex
main do
  let n = 4
  let size = n > 3 then "big" else "small"
  IO.printLine(size)
end
```
