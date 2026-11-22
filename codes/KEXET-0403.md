---
title: KEXET-0403
---

Inside a `make` block for a record, `new` starts as a copy of `this` that
you can change field by field. `Integer` is not a record and has no fields,
so `make Integer` has no `new`.

```kex
make Integer do
  let doubled -> Integer = new * 2
end
```

```
example.kex:2:28: [KEXET-0403]: Error, `new` requires a record receiver
  |
2 |   let doubled -> Integer = new * 2
  |                            ^^^
```

## Fixing it

Use `this`, which is the number itself:

```kex
make Integer do
  let doubled -> Integer = this * 2
end

main do
  IO.printLine(21.doubled)
end
```

`New { ... }` has the same rule; see [KEXET-0450](../KEXET-0450/).
