---
title: KEXET-0421
---

There is no module called `Strng`. It is a typo for `String`.

```kex
main do
  IO.printLine(Strng.upperCase("hi"))
end
```

```
example.kex:2:16: [KEXET-0421]: Error, unknown module `Strng`
  |
2 |   IO.printLine(Strng.upperCase("hi"))
  |                ^^^^^
```

If the module exists but the function does not, the error is
[KEXET-0423](../KEXET-0423/).

## Fixing it

```kex
main do
  IO.printLine(String.upperCase("hi"))
end
```

Bare `kex -s` lists every module in the standard library. A module of your
own has to be imported before you use it.
