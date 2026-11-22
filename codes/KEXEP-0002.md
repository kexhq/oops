---
title: KEXEP-0002
---

`:>` is the signature arrow for methods. In a `make Integer` block,
`double :> Integer` would mean "takes the `Integer` it is called on and
gives an `Integer`". `double` here is a plain function at the top level,
where there is no type to call it on.

```kex
double :> Integer -> Integer
let double(n) = n * 2
```

```
example.kex:1:1: [KEXEP-0002]: Error, ':>' (implicit-This signature) is only valid inside 'make T do ... end'. Use ':' at top level instead
  |
1 | double :> Integer -> Integer
  | ^^^^^^
```

## Fixing it

Use `:`:

```kex
double : Integer -> Integer
let double(n) = n * 2

main do
  IO.printLine(double(21))
end
```
