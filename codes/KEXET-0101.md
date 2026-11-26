---
title: KEXET-0101
---

`String` has no function `upcase`. Kex reads a lot like Ruby, but many names
are different: it is `upperCase` here, and `count` where Ruby has `size`.

```kex
main do
  IO.printLine("hello".upcase)
end
```

```
example.kex:2:30: [KEXET-0101]: Error, undefined function `upcase` for `String`
  |
2 |   IO.printLine("hello".upcase)
  |                ^^^^^^^^^^^^^^
```

## Fixing it

```kex
main do
  IO.printLine("hello".upperCase)
end
```

`kex -s String` lists every function `String` has.
