---
title: KEXEP-0001
---

`break` is a keyword, so a function cannot be called that. The same goes
for `return`, `then`, `while`, `when`, `if`, `do` and `end`, among others.

```kex
let break(text: String) -> [String] = text.split(" ")
```

```
example.kex:1:5: [KEXEP-0001]: Error, `break` is a reserved keyword in Kex, so it cannot name a function. Rename it
  |
1 | let break(text: String) -> [String] = text.split(" ")
  |     ^^^^^
```

A keyword used as a variable name is [KEXEP-0124](../KEXEP-0124/).

## Fixing it

Pick another name:

```kex
let words(text: String) -> [String] = text.split(" ")

main do
  IO.printLine(words("a few words"))
end
```
