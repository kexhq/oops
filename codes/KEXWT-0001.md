---
title: KEXWT-0001
---

The type line above `add` gives it one parameter, and the definition has
two. This is a warning, so the program still compiles, but the type line
does not say what `add` really takes.

```kex
add : Integer -> Integer
let add(a, b) = a + b

main do
  IO.printLine(add(1, 2))
end
```

```
example.kex:2:1: [KEXWT-0001]: Warning, type annotation for 'add' declares 1 parameter(s) but definition has 2
  |
2 | let add(a, b) = a + b
  | ^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

A function of two parameters has two arrows before the result:

```kex
add : Integer -> Integer -> Integer
let add(a, b) = a + b

main do
  IO.printLine(add(1, 2))
end
```
