---
title: KEXET-0128
---

Every `String` already has `count` from the standard library. Defining
another one in a `make String` block would make `"text".count` ambiguous,
so it is rejected.

```kex
make String do
  let count -> Integer = 0
end
```

```
example.kex:2:3: [KEXET-0128]: Error, `count` is defined twice for receiver `String`: here and in the prelude
  |
2 |   let count -> Integer = 0
  |   ^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Give your function its own name:

```kex
make String do
  let wordCount -> Integer = this.split(" ").count
end

main do
  IO.printLine("a few words".wordCount)
end
```
