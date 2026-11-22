---
title: KEXEP-0101
---

A single capital letter, such as `N`, is reserved for type parameters, as
in `[X]`. A variable cannot be called that.

```kex
main do
  let N = 10
  IO.printLine(N * 2)
end
```

```
example.kex:2:7: [KEXEP-0101]: Error, cannot bind 'N': single-letter uppercase names are reserved for type parameters
  |
2 |   let N = 10
  |       ^
```

A record or type with a one-letter name gets [KEXEP-0020](../KEXEP-0020/)
or [KEXEP-0011](../KEXEP-0011/).

## Fixing it

Use a lowercase name:

```kex
main do
  let n = 10
  IO.printLine(n * 2)
end
```
