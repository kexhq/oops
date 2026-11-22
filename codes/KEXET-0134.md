---
title: KEXET-0134
---

`count` is a `var`, and a `let` with the same name cannot be declared
after it in the same block.

```kex
main do
  var count = 1
  let count = 2
  IO.printLine(count)
end
```

```
example.kex:3:3: [KEXET-0134]: Error, cannot redeclare 'count': was declared with 'var'
  |
3 |   let count = 2
  |   ^^^^^^^^^^^^^
```

Declaring a `let` twice is [KEXET-0135](../KEXET-0135/).

## Fixing it

To change the value, assign to the `var`:

```kex
main do
  var count = 1
  count = 2
  IO.printLine(count)
end
```

If you meant a separate value, give it its own name.
