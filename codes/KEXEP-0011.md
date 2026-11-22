---
title: KEXEP-0011
---

`T` is a single capital letter, which Kex keeps for type parameters, as in
`[T]`. A type needs a longer name.

```kex
type T = Small | Large
```

```
example.kex:1:8: [KEXEP-0011]: Error, `T` is a type parameter, so it cannot name a type. Give it a longer name
  |
1 | type T = Small | Large
  |        ^
```

The same rule gives [KEXEP-0020](../KEXEP-0020/) for a record and
[KEXEP-0101](../KEXEP-0101/) for a variable.

## Fixing it

```kex
type Size = Small | Large

main do
  IO.printLine(Small)
end
```
