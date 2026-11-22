---
title: KEXET-0485
---

`greeting` was declared with no parameters, and it was called with one.

```kex
let greeting -> String = "hello"

main do
  IO.printLine(greeting("Ada"))
end
```

```
example.kex:4:16: [KEXET-0485]: Error, `greeting` takes no arguments, got 1
  |
4 |   IO.printLine(greeting("Ada"))
  |                ^^^^^^^^^^^^^^^
```

## Fixing it

If it should take a name, give it a parameter:

```kex
let greeting(name: String) -> String = "hello, ${name}"

main do
  IO.printLine(greeting("Ada"))
end
```

If it should not, call it with no arguments and no parentheses:
`greeting`.
