---
title: KEXET-0472
---

`add` takes two arguments, and it was called with one.

```kex
let add(a: Integer, b: Integer) -> Integer = a + b

main do
  IO.printLine(add(1))
end
```

```
example.kex:4:16: [KEXET-0472]: Error, `add` expects 2 argument(s), got 1
  |
4 |   IO.printLine(add(1))
  |                ^^^^^^
```

In a call with a dot, the value before the dot is the first argument, so
`list.take(2)` passes two.

## Fixing it

```kex
let add(a: Integer, b: Integer) -> Integer = a + b

main do
  IO.printLine(add(1, 2))
end
```
