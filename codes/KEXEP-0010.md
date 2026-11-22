---
title: KEXEP-0010
---

Type names start with a capital letter. `shape` is lowercase, so the
parser does not read it as a type name.

```kex
type shape = Circle(Float) | Square(Float)
```

```
example.kex:1:6: [KEXEP-0010]: Error, expected type name, got LowerIdent [shape]
  |
1 | type shape = Circle(Float) | Square(Float)
  |      ^^^^^
```

## Fixing it

```kex
type Shape = Circle(Float) | Square(Float)

main do
  IO.printLine(Circle(1.0))
end
```
