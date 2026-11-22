---
title: KEXEP-0097
---

A `while` condition is followed by `do`, as in `while n < 3 do`.

```kex
main do
  var n = 0
  while n < 3
    n += 1
  end
  IO.printLine(n)
end
```

```
example.kex:3:14: [KEXEP-0097]: Error, expected 'do' after 'while' condition, got Newline
  |
3 |   while n < 3
  |              ^
```

## Fixing it

```kex
main do
  var n = 0
  while n < 3 do
    n += 1
  end
  IO.printLine(n)
end
```
