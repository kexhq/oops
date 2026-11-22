---
title: KEXEP-0064
---

`...parts` spreads a list into another list, as in `[...parts, "!"]`. It
cannot spread a list into the arguments of a call, so `greet` does not get
`"Ada"` and `"Lovelace"` this way.

```kex
let greet(first: String, last: String) = "hello, ${first} ${last}"

main do
  let parts = ["Ada", "Lovelace"]
  IO.printLine(greet(...parts))
end
```

```
example.kex:5:22: [KEXEP-0064]: Error, `...` only spreads into a list, a map, or a `do` block body
  |
5 |   IO.printLine(greet(...parts))
  |                      ^^^
```

## Fixing it

Take the list apart first, and pass the pieces:

```kex
let greet(first: String, last: String) = "hello, ${first} ${last}"

main do
  let parts = ["Ada", "Lovelace"]
  let [first, last] = parts
  IO.printLine(greet(first, last))
end
```

If `greet` should work on any number of names, make it take the list:
`let greet(parts: [String])`.
