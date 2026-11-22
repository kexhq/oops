---
title: KEXET-0121
---

The line `double : Integer -> Integer` says `double` returns an
`Integer`. The definition below it says `-> String`. They cannot both be
right.

```kex
double : Integer -> Integer
let double(n: Integer) -> String = "${n * 2}"

main do
  IO.printLine(double(4))
end
```

```
example.kex:2:27: [KEXET-0121]: Error, inline return type for `double` disagrees with its separate annotation: String versus Integer
  |
2 | let double(n: Integer) -> String = "${n * 2}"
  |                           ^^^^^^
example.kex:2:36: [KEXET-0127]: Error, `double` declared to return Integer but body returns String
  |
2 | let double(n: Integer) -> String = "${n * 2}"
  |                           ------   ^^^^^^^^^^ this has type String
  |                           |
  |                           expected because of this return type
```

The second error comes from the same line: the body is checked against
the annotation above it.

## Fixing it

With a separate annotation, the definition does not need its own return
type. Drop it, and make the body fit the annotation:

```kex
double : Integer -> Integer
let double(n: Integer) = n * 2

main do
  IO.printLine(double(4))
end
```

If `double` should return text, change the annotation to
`Integer -> String` instead.
