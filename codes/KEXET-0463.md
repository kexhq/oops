---
title: KEXET-0463
---

`+` cannot add a `String` and an `Integer`. Kex does not turn the number
into text for you.

```kex
main do
  let count = 3
  IO.printLine("total: " + count)
end
```

```
example.kex:3:28: [KEXET-0463]: Error, cannot add String and Integer
  |
3 |   IO.printLine("total: " + count)
  |                ^^^^^^^^^^^^^^^^^
```

## Fixing it

Put the number into the string with `${...}`:

```kex
main do
  let count = 3
  IO.printLine("total: ${count}")
end
```

If you meant to add two numbers and one of them is text, convert it with
`.to(Integer)`. That gives an optional, so add `.or(...)` with the value to
use when the text is not a number.
