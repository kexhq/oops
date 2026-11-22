---
title: KEXET-0411
---

`count` was made with `let`, so it cannot be given a new value. Only a
`var` can.

```kex
main do
  let count = 0
  count = count + 1
  IO.printLine(count)
end
```

```
example.kex:3:3: [KEXET-0411]: Error, cannot assign to immutable binding: count
  |
3 |   count = count + 1
  |   ^^^^^^^^^^^^^^^^^
```

Calling a `!` method on a `let`, such as `names.push!`, is the same mistake,
reported as [KEXET-0425](../KEXET-0425/).

## Fixing it

Make it a `var`:

```kex
main do
  var count = 0
  count = count + 1
  IO.printLine(count)
end
```

Often you do not need to change it at all. A new `let` with its own name,
`let total = count + 1`, keeps both values around.
