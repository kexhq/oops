---
title: KEXET-0163
---

There is no function called `shout` in this file, in the standard library,
or in any module imported here.

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

Write the function, or import the module it comes from:

```kex
let shout(text: String) -> String = "${text.upperCase}!"

main do
  IO.printLine(shout("hi"))
end
```

`kex -s shout` tells you whether the standard library has anything by that
name.
