---
title: KEXET-0482
---

`greet` has no parameter called `lod?`, but it has one called `loud?`, so
the compiler suggests that.

```kex
let greet(name: String, loud?: Bool = false) -> String = loud? then name.upperCase else name

main do
  IO.printLine(greet("Ada", lod?: true))
end
```

```
example.kex:4:16: [KEXET-0482]: Error, unknown named argument `lod?:` for `greet`, did you mean `loud?:`?
  |
4 |   IO.printLine(greet("Ada", lod?: true))
  |                ^^^^^^^^^^^^^^^^^^^^^^^^
```

With no close name to suggest, the error is [KEXET-0481](../KEXET-0481/).

## Fixing it

```kex
let greet(name: String, loud?: Bool = false) -> String = loud? then name.upperCase else name

main do
  IO.printLine(greet("Ada", loud?: true))
end
```
