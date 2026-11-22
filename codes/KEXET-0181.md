---
title: KEXET-0181
---

`level` is an `Integer`, and it could be any size. A `Byte` holds only 0
to 255. `.as` converts without checking, so it is not allowed here.

```kex
main do
  let level = 200
  let byte = level.as(Byte)
  IO.printLine(byte)
end
```

```
example.kex:3:22: [KEXET-0181]: Error, unchecked narrowing to Byte is not allowed; use `.to(Byte)`
  |
3 |   let byte = level.as(Byte)
  |              ^^^^^^^^^^^^^^
```

The same happens with a literal: `200.as(Byte)` is also rejected.

## Fixing it

`.to(Byte)` checks the range and gives a `Byte?`, which is empty when the
number does not fit. Decide what to use then:

```kex
main do
  let level = 200
  let byte = level.to(Byte).or(255)
  IO.printLine(byte)
end
```

For a fixed number, write it where a `Byte` is expected, as in
`let byte: Byte = 200`.
