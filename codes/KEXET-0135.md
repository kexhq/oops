---
title: KEXET-0135
---

`total` already exists in this block, and a `let` cannot be declared
twice. Ruby lets you reuse a name for a new value; Kex does not.

```kex
main do
  let total = 10
  let total = total + 5
  IO.printLine(total)
end
```

```
example.kex:3:3: [KEXET-0135]: Error, cannot redeclare immutable binding: total
  |
3 |   let total = total + 5
  |   ^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Give the new value its own name:

```kex
main do
  let total = 10
  let withTax = total + 5
  IO.printLine(withTax)
end
```

If the value really has to change over time, make it a `var` and
assign to it.
