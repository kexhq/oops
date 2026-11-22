---
title: KEXET-0479
---

A bare `parse` could be one of several functions the prelude brings in.
`Kex.Date` has one, `Kex.DateFormat` has another, and neither is the one
for numbers.

```kex
main do
  let year = parse("2024")
  IO.printLine(year)
end
```

```
example.kex:2:14: [KEXET-0479]: Error, ambiguous imported function 'parse' is provided by both 'Kex.Date' and 'Kex.DateFormat'
  |
2 |   let year = parse("2024")
  |              ^^^^^^^^^^^^^
```

## Fixing it

Write the type in front of it. `Integer.parse` gives a `Result`, so `.or`
supplies a number for text that does not parse:

```kex
main do
  let year = Integer.parse("2024").or(0)
  IO.printLine(year + 1)
end
```

A `parse` you declare yourself, with the same number of arguments, is used
instead of the imported ones.
