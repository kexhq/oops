---
title: KEXET-0481
---

`greet` has no parameter called `shout`. A named argument has to use the
name of one of the function's parameters, here `loud?`.

```kex
let greet(name: String, loud?: Bool = false) -> String = loud? then name.upperCase else name

main do
  IO.printLine(greet("Ada", shout: true))
end
```

```
example.kex:4:16: [KEXET-0481]: Error, unknown named argument `shout:` for `greet`
  |
4 |   IO.printLine(greet("Ada", shout: true))
  |                ^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

```kex
let greet(name: String, loud?: Bool = false) -> String = loud? then name.upperCase else name

main do
  IO.printLine(greet("Ada", loud?: true))
end
```
