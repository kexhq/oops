---
title: KEXET-0168
---

`lib/kitchen.kex` declares `portions` below the `Kitchen` module, not inside
it. A function there belongs to that file, so `Kitchen` itself can call it,
but `using Kitchen` does not bring it in.

`lib/kitchen.kex`:

```kex
module Kitchen do
  let servings() -> Integer = portions() * 2
end

let portions() -> Integer = 4
```

`example.kex`:

```kex
using Kitchen

main do
  IO.printLine(servings())
  IO.printLine(portions())
end
```

```
example.kex:5:16: [KEXET-0168]: Error, undefined function: `portions`. kitchen.kex declares it outside its module, for itself
  |
5 |   IO.printLine(portions())
  |                ^^^^^^^^^^
```

A type or constructor declared the same way gives
[KEXET-0157](../KEXET-0157/).

## Fixing it

Move `portions` inside the module. `example.kex` stays as it is:

```kex
module Kitchen do
  let servings() -> Integer = portions() * 2
  let portions() -> Integer = 4
end
```
