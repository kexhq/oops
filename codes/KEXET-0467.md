---
title: KEXET-0467
---

`input` is a `String`, and `9` is an `Integer`. Kex does not compare a
string with a number, even when the string holds digits.

```kex
main do
  let input = "10"
  IO.printLine(input > 9)
end
```

```
example.kex:3:24: [KEXET-0467]: Error, cannot compare String and Integer
  |
3 |   IO.printLine(input > 9)
  |                ^^^^^^^^^
```

## Fixing it

Convert the string first:

```kex
main do
  let input = "10"
  IO.printLine(input.to(Integer).or(0) > 9)
end
```
