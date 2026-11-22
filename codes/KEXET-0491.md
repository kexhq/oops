---
title: KEXET-0491
---

`double` takes an `Integer`, and it was given a `String`. Arguments are
counted from 1, and the function's signature is printed under the message.

```kex
let double(n: Integer) -> Integer = n * 2

main do
  IO.printLine(double("4"))
end
```

```
example.kex:4:16: [KEXET-0491]: Error, `double` expects argument 1 to be Integer, but got String

double : Integer -> Integer
  |
4 |   IO.printLine(double("4"))
  |                ^^^^^^^^^^^
```

A `let` whose value does not fit its annotation is
[KEXET-0001](../KEXET-0001/). Too many or too few arguments is
[KEXET-0472](../KEXET-0472/).

## Fixing it

Pass an `Integer`. Text has to be converted, with a fallback for when it is
not a number:

```kex
let double(n: Integer) -> Integer = n * 2

main do
  IO.printLine(double("4".to(Integer).or(0)))
end
```

Or change the parameter's type, if that is the part that is wrong.
