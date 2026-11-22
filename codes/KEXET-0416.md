---
title: KEXET-0416
---

`+` is not defined for `Money`. The compiler does not know how to add two
records, so it asks you to say how.

```kex
record Money do
  cents : Integer
end

main do
  let price = Money { cents: 250 }
  let tax = Money { cents: 50 }
  IO.printLine((price + tax).cents)
end
```

```
example.kex:8:25: [KEXET-0416]: Error, `+` is not defined for Money and Money; declare it in a `make Money` block
  |
8 |   IO.printLine((price + tax).cents)
  |                ^^^^^^^^^^^^^
```

## Fixing it

Define the operator in a `make Money` block. An operator is a function
named by the operator:

```kex
record Money do
  cents : Integer
end

make Money do
  let +(other: This) -> This = New { cents: @cents + other.cents }
end

main do
  let price = Money { cents: 250 }
  let tax = Money { cents: 50 }
  IO.printLine((price + tax).cents)
end
```
