---
title: KEXEP-0124
---

`next` is a keyword, so a variable cannot be called that, not even one
bound by taking a tuple apart. The same goes for `return`, `match`,
`break`, `then`, `loop` and `when`, among others.

```kex
main do
  let (first, next) = (1, 2)
  IO.printLine(first + next)
end
```

```
example.kex:2:15: [KEXEP-0124]: Error, `next` is a reserved keyword in Kex, so it cannot name a variable. Rename it
  |
2 |   let (first, next) = (1, 2)
  |               ^^^^
```

A plain `let next = 1` is read as a definition and reported as
[KEXEP-0001](../KEXEP-0001/).

## Fixing it

Pick another name:

```kex
main do
  let (first, second) = (1, 2)
  IO.printLine(first + second)
end
```
