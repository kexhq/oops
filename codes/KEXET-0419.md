---
title: KEXET-0419
---

`!` turns a `Bool` around, and `items.count` is an `Integer`. Kex does not
treat `0` as false.

```kex
main do
  let items = [1, 2]
  IO.printLine(!items.count)
end
```

```
example.kex:3:16: [KEXET-0419]: Error, logical not '!' requires Bool, got Integer
  |
3 |   IO.printLine(!items.count)
  |                ^^^^^^^^^^^^
```

## Fixing it

Ask the question you mean, as a `Bool`:

```kex
main do
  let items = [1, 2]
  IO.printLine(!items.empty?)
end
```
