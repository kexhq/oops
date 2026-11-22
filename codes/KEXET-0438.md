---
title: KEXET-0438
---

Every element of a list has the same type. The first element, `1`, makes
this a list of `Integer`s, so `"two"` does not fit.

```kex
main do
  let row = [1, "two", 3]
  IO.printLine(row)
end
```

```
example.kex:2:13: [KEXET-0438]: Error, list elements must be the same type. Expected Integer, got String
  |
2 |   let row = [1, "two", 3]
  |             ^^^^^^^^^^^^^
```

## Fixing it

Make the elements agree:

```kex
main do
  let row = [1, 2, 3]
  IO.printLine(row)
end
```

To keep a few values of different types together, use a tuple, as in
`(1, "two", 3)`, or a record.
