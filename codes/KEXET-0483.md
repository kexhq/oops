---
title: KEXET-0483
---

`greet` takes a `name` and a `greeting`, and the call gives only the
`greeting`. A parameter with no default has to be passed.

```kex
let greet(name: String, greeting: String) -> String = "${greeting}, ${name}"

main do
  IO.printLine(greet(greeting: "Hello"))
end
```

```
example.kex:4:16: [KEXET-0483]: Error, missing required argument `name` for `greet`
  |
4 |   IO.printLine(greet(greeting: "Hello"))
  |                ^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

```kex
let greet(name: String, greeting: String) -> String = "${greeting}, ${name}"

main do
  IO.printLine(greet("Ada", greeting: "Hello"))
end
```

If most calls leave it out, give the parameter a default in the function,
as `loud?: Bool = false` has in [KEXET-0482](../KEXET-0482/).
