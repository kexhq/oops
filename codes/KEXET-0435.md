---
title: KEXET-0435
---

`~anonymous` is the function itself, not a call to it. `.or` never calls
what it is given, so the answer would be the function, not a `String`.

```kex
let anonymous(id: Integer) -> String = "user ${id}"

main do
  let names = ["ada", "alan"]
  IO.printLine(names.first.or(~anonymous))
end
```

```
example.kex:5:31: [KEXET-0435]: Error, `or` needs a fallback of type String, but got a function. `or` never calls it, so the function itself would be the answer; pass a plain default, or `match` on the optional to compute one
  |
5 |   IO.printLine(names.first.or(~anonymous))
  |                               ^^^^^^^^^^
```

A block in the same place is [KEXET-0433](../KEXET-0433/).

## Fixing it

Call the function, and pass what it returns:

```kex
let anonymous(id: Integer) -> String = "user ${id}"

main do
  let names = ["ada", "alan"]
  IO.printLine(names.first.or(anonymous(0)))
end
```
