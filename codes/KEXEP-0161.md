---
title: KEXEP-0161
---

`=` gives a function a body that fits on the same line. `greet`'s body is
on the line after the `=`, and a body on its own line goes in a `do` block.

```kex
let greet(name: String) -> String =
  "Hello, ${name}!"

main do
  IO.printLine(greet("Ada"))
end
```

```
example.kex:1:35: [KEXEP-0161]: Error, a function body on its own line goes in `do ... end`: write `do` in place of `=`, and `end` after the body
  |
1 | let greet(name: String) -> String =
  |                                   ^
```

## Fixing it

Write `do` in place of `=`, and close the body with `end`:

```kex
let greet(name: String) -> String do
  "Hello, ${name}!"
end

main do
  IO.printLine(greet("Ada"))
end
```

A body this short can also stay on the `=` line:
`let greet(name: String) -> String = "Hello, ${name}!"`.
