---
title: KEXEP-0020
---

A single capital letter, like `P`, is a type parameter, as in `[X]` or
`X?`. It cannot also be the name of a record.

```kex
record P do
  x : Integer
  y : Integer
end
```

```
example.kex:1:10: [KEXEP-0020]: Error, `P` is a type parameter, so it cannot name a record. Give it a longer name
  |
1 | record P do
  |          ^^
```

## Fixing it

Give the record a name that is longer than one letter:

```kex
record Point do
  x : Integer
  y : Integer
end

main do
  IO.printLine(Point { x: 1, y: 2 }.x)
end
```
