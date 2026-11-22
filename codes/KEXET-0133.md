---
title: KEXET-0133
---

`count` is already a `var`, and a second `var count` in the same block
cannot declare it again. To give it a new value, assign to it.

```kex
main do
  var count = 0
  var count = 1
  IO.printLine(count)
end
```

```
example.kex:3:3: [KEXET-0133]: Error, cannot redeclare 'count': already declared with 'var'
  |
3 |   var count = 1
  |   ^^^^^^^^^^^^^
```

A `let` with the name of an earlier `var` is [KEXET-0134](../KEXET-0134/),
and a `let` declared twice is [KEXET-0135](../KEXET-0135/).

## Fixing it

```kex
main do
  var count = 0
  count = 1
  IO.printLine(count)
end
```
