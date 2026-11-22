---
title: KEXET-0164
---

There is no function called `shuot`, but there is one called `shout`, so the
compiler guesses that is the one you meant.

```kex
let shout(text: String) -> String = "${text.upperCase}!"

main do
  IO.printLine(shuot("hi"))
end
```

```
example.kex:4:16: [KEXET-0164]: Error, undefined function: `shuot`, did you mean `shout`?
  |
4 |   IO.printLine(shuot("hi"))
  |                ^^^^^^^^^^^
```

With no close match, the error is [KEXET-0163](../KEXET-0163/).

## Fixing it

```kex
let shout(text: String) -> String = "${text.upperCase}!"

main do
  IO.printLine(shout("hi"))
end
```
