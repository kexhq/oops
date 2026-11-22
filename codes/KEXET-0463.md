---
title: KEXET-0463
---

`+` was used on two values that can't be added together. Most often it's
text and a number. Kex doesn't turn a number into text on its own.

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

Put the value in the text with `${...}`:

```kex
main do
  let count = 3
  IO.printLine("total: ${count}")
end
```

If you meant to add numbers, one side is the wrong type. Text that holds a
number becomes one with `.to(Integer)`, which gives an optional, so add
`.or(...)` with a value to use when it isn't a number.
