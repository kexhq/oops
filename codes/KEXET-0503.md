---
title: KEXET-0503
---

`shout`'s parameter has no type, so `shout` takes anything that has an
`upperCase`. `42` is an `Integer`, which has none.

```kex
let shout(text) = text.upperCase

main do
  IO.printLine(shout("hi"))
  IO.printLine(shout(42))
end
```

```
example.kex:5:16: [KEXET-0503]: Error, `shout` calls `upperCase` on its argument 1, and Integer has no `upperCase`
  |
5 |   IO.printLine(shout(42))
  |                ^^^^^^^^^
```

With a type on the parameter, the same call is
[KEXET-0491](../KEXET-0491/).

## Fixing it

Pass a value that has the function:

```kex
let shout(text) = text.upperCase

main do
  IO.printLine(shout("hi"))
  IO.printLine(shout("${42}"))
end
```

Or give the parameter a type, so the function says what it takes:

```kex
let shout(text: String) -> String = text.upperCase

main do
  IO.printLine(shout("hi"))
end
```
