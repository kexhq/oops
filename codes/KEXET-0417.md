---
title: KEXET-0417
---

`first` and `second` are known only as `Priced`. The trait gives them a
`price`, but it says nothing about `+`, so there is no way to add two of
them.

```kex
trait Priced do
  price :> Integer
end

let total(first: Priced, second: Priced) -> Integer = first + second
```

```
example.kex:5:63: [KEXET-0417]: Error, `+` is not defined for Priced and Priced; declare it in trait `Priced`
  |
5 | let total(first: Priced, second: Priced) -> Integer = first + second
  |                                                       ^^^^^^^^^^^^^^
```

For a record or type of your own, the same error is
[KEXET-0416](../KEXET-0416/).

## Fixing it

What `total` wants is the sum of the two prices, and those are integers:

```kex
trait Priced do
  price :> Integer
end

record Book do
  cents : Integer
end

make Book, implement: Priced do
  let price -> Integer = @cents
end

let total(first: Priced, second: Priced) -> Integer = first.price + second.price

main do
  IO.printLine(total(Book { cents: 1200 }, Book { cents: 950 }))
end
```

If every `Priced` value really should support `+`, add it to the trait
with `+ :> This -> This`. Then each type that implements `Priced` has to
define it.
