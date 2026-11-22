---
title: KEXET-0468
---

`||` works on two `Bool`s. Here it was used to pick a default for a
missing value, which is a Ruby habit. Each side that is not a `Bool` gets
its own error.

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first || "nobody")
end
```

```
example.kex:3:25: [KEXET-0468]: Error, logical operator requires Bool, got String?
  |
3 |   IO.printLine(first || "nobody")
  |                ^^^^^^^^^^^^^^^^^
example.kex:3:25: [KEXET-0468]: Error, logical operator requires Bool, got String
  |
3 |   IO.printLine(first || "nobody")
  |                ^^^^^^^^^^^^^^^^^
```

## Fixing it

`.or` gives the value if there is one, and the default otherwise:

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first.or("nobody"))
end
```
