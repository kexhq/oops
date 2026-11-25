---
title: KEXET-0498
---

`count` is an `Integer` and `"1"` is a `String`. A value of one type is never
equal to a value of an unrelated one, so this comparison would always be
`false`.

```kex
main do
  let count = 1
  IO.printLine(count == "1")
end
```

```
example.kex:3:25: [KEXET-0498]: Error, `Integer` and `String` are never equal: values of unrelated types
  |
3 |   IO.printLine(count == "1")
  |                ^^^^^^^^^^^^
```

An `Integer` and a `Float` can be compared (`1 == 1.0` is `true`). An
optional compared with a plain value is [KEXET-0494](../KEXET-0494/).

## Fixing it

Compare values of the same type, converting one of them:

```kex
main do
  let count = 1
  IO.printLine("${count}" == "1")
end
```
