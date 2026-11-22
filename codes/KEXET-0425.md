---
title: KEXET-0425
---

A method ending in `!` changes the variable it is called on, and `names` is
a `let`, which cannot change.

```kex
main do
  let names = ["ada"]
  names.push!("alan")
  IO.printLine(names)
end
```

```
example.kex:3:14: [KEXET-0425]: Error, cannot use '!' on immutable binding: names
  |
3 |   names.push!("alan")
  |   ^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Make it a `var`:

```kex
main do
  var names = ["ada"]
  names.push!("alan")
  IO.printLine(names)
end
```

Or keep the `let` and make a new list, `let more = [...names, "alan"]`.
