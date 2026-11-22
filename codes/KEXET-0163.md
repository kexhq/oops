---
title: KEXET-0163
---

The code calls a function that doesn't exist: not in this file, not in the
standard library, and not in anything imported.

```kex
main do
  IO.printLine(shout("hi"))
end
```

```
example.kex:2:16: [KEXET-0163]: Error, undefined function: `shout`
  |
2 |   IO.printLine(shout("hi"))
  |                ^^^^^^^^^^^
```

## Fixing it

Define the function, or import the module that has it:

```kex
let shout(text: String) -> String = "${text.upperCase}!"

main do
  IO.printLine(shout("hi"))
end
```

If you expected the standard library to have it, look it up. `kex -s shout`
finds a name on every type and module, and `kex -s String` lists everything
a `String` can do.
