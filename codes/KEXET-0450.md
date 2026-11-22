---
title: KEXET-0450
---

`New { ... }` copies `this` with some fields changed. `Size` is a type
with two variants, `Small` and `Large`, and neither has fields, so there is
nothing for `New` to copy.

```kex
type Size = Small | Large

make Size do
  let bigger -> Size = New { }
end
```

```
example.kex:4:24: [KEXET-0450]: Error, `New` requires a record receiver
  |
4 |   let bigger -> Size = New { }
  |                        ^^^^^^^
```

## Fixing it

Build the value you want by name. For a type like `Size`, that usually
means a `match`:

```kex
type Size = Small | Large

make Size do
  let bigger -> Size = match this do
    Small => Large
    Large => Large
  end
end

main do
  IO.printLine(Small.bigger)
end
```

`New` works in a `make` block for a `record`.
