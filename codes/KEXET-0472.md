---
title: KEXET-0472
---

A function was called with the wrong number of arguments. The message gives
how many it takes and how many it got.

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

With method syntax, the value before the dot counts as the first argument.
`list.take(2)` is `take(list, 2)`, which is two arguments.

## Fixing it

Pass every argument the function takes:

```kex
let add(a: Integer, b: Integer) -> Integer = a + b

main do
  IO.printLine(add(1, 2))
end
```
