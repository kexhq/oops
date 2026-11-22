---
title: KEXEP-0058
---

A type parameter, which stands for any type, is a single capital letter.
`x` is lowercase.

```kex
let firstOr(items: [x], fallback: x) -> x = items.first.or(fallback)
```

```
example.kex:1:21: [KEXEP-0058]: Error, type parameters are uppercase: write `X` rather than `x`
  |
1 | let firstOr(items: [x], fallback: x) -> x = items.first.or(fallback)
  |                     ^
```

## Fixing it

```kex
let firstOr(items: [X], fallback: X) -> X = items.first.or(fallback)

main do
  IO.printLine(firstOr([], 7))
end
```
