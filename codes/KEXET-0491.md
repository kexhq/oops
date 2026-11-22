---
title: KEXET-0491
---

A function was called with an argument of the wrong type. The message says
which argument, counting from 1, what type the function wants there, and what
it got. Under the message is the function's signature.

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

When a function has several signatures, all of them are listed, so you can
see which one you meant.

A `let` whose value doesn't match its annotation is
[KEXET-0001](../KEXET-0001/). Too many or too few arguments is
[KEXET-0472](../KEXET-0472/).

## Fixing it

Pass a value of the right type. Here the text has to be turned into a
number first, and you choose what to use when it isn't one:

```kex
let double(n: Integer) -> Integer = n * 2

main do
  IO.printLine(double("4".to(Integer).or(0)))
end
```

If the function should take this type too, change its parameter instead.
