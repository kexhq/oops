---
title: KEXET-0495
---

A function whose name ends in `!` changes the variable it is called on:
`items.sort!` sorts `items` in place. Here it is called on a list written
out directly, so there is no variable for it to change.

```kex
main do
  IO.printLine([3, 1].sort!)
end
```

```
example.kex:2:28: [KEXET-0495]: Error, `sort!` rewrites the `var` it is called on, and this receiver is no variable: bind it with `var` first
  |
2 |   IO.printLine([3, 1].sort!)
  |                ^^^^^^^^^^^^
```

The same call on a `let` binding, which cannot change, is
[KEXET-0425](../KEXET-0425/).

## Fixing it

Bind the value with `var` first:

```kex
main do
  var items = [3, 1]
  items.sort!
  IO.printLine(items)
end
```

Or call the version without `!`, which gives back a new list:

```kex
main do
  IO.printLine([3, 1].sort)
end
```
