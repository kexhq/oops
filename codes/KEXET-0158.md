---
title: KEXET-0158
---

`count = 1` gives a new value to a variable, and there is no variable called
`count`. Kex has no assignment that also creates the variable, as Ruby
does.

```kex
main do
  count = 1
end
```

```
example.kex:2:3: [KEXET-0158]: Error, undefined variable: `count`
  |
2 |   count = 1
  |   ^^^^^^^^^
```

## Fixing it

Declare it first. A `var` can be given new values later:

```kex
main do
  var count = 0
  count = 1
  IO.printLine(count)
end
```

If the value never changes, `let count = 1` is enough.
