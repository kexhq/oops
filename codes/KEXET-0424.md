---
title: KEXET-0424
---

The code calls `Module.name`, the module has no function by that name, and
one of its functions is spelled almost the same. The message suggests it.

```kex
main do
  IO.println("hi")
end
```

```
example.kex:2:13: [KEXET-0424]: Error, `IO` has no function `println`, did you mean `print`?
  |
2 |   IO.println("hi")
  |   ^^^^^^^^^^^^^^^^
```

The suggestion is only the closest spelling, so it isn't always the right
one. `IO.print` writes without a newline, while `println` in other
languages ends the line, so here you want `IO.printLine`.

## Fixing it

```kex
main do
  IO.printLine("hi")
end
```

`kex -s IO` lists all of the module's functions.
