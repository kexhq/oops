---
title: KEXET-0116
---

`Point` has two fields, `x` and `y`. Written like a constructor,
`Point(x)` names only one value, so it does not fit.

```kex
record Point do
  x : Integer
  y : Integer
end

main do
  let Point(x) = Point { x: 1, y: 2 }
  IO.printLine(x)
end
```

```
example.kex:7:7: [KEXET-0116]: Error, `Point` record takes 2 value(s), but the pattern destructures 1
  |
7 |   let Point(x) = Point { x: 1, y: 2 }
  |       ^^^^^^^^
```

The same mistake on a constructor of a `type`, such as `Just(a, b)`, is
[KEXET-0114](../KEXET-0114/).

## Fixing it

To take only some of the fields, name them in braces:

```kex
record Point do
  x : Integer
  y : Integer
end

main do
  let Point { x } = Point { x: 1, y: 2 }
  IO.printLine(x)
end
```

The positional form has to list every field, in the order the record
declares them: `Point(x, _)`.
