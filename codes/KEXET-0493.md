---
title: KEXET-0493
---

A `Byte` holds a number from 0 to 255. `size` is a list of bytes, so
`300` cannot go in it.

```kex
main do
  let size: [Byte] = [0, 300]
  IO.printLine(size.count)
end
```

```
example.kex:2:26: [KEXET-0493]: Error, Byte literal must be in 0..255
  |
2 |   let size: [Byte] = [0, 300]
  |                          ^^^
```

A negative number such as `-1` gets the same error.

## Fixing it

A number above 255 takes more than one byte. 300 is 1 × 256 + 44, so as
two bytes, high byte first, it is `1` and `44`:

```kex
main do
  let size: [Byte] = [1, 44]
  IO.printLine(size.count)
end
```

If the list was never meant to hold bytes, make it an `[Integer]`.
