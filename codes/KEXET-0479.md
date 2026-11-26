---
title: KEXET-0479
---

After `using Date` and `using DateFormat`, a bare `parse` could be either
module's, and neither is the one for numbers. The second `using` is
rejected for bringing in a name the first already did, which is
[KEXET-0140](../KEXET-0140/), and the call is ambiguous as well.

```kex
using Date
using DateFormat

main do
  let year = parse("2024")
  IO.printLine(year)
end
```

```
example.kex:2:1: [KEXET-0140]: Error, ambiguous name `parse`, imported from both `Date` and `DateFormat`
  |
2 | using DateFormat
  | ^^^^^^^^^^^^^^^^
example.kex:5:14: [KEXET-0479]: Error, ambiguous imported function 'parse' is provided by both 'Kex.Date' and 'Kex.DateFormat'
  |
5 |   let year = parse("2024")
  |              ^^^^^^^^^^^^^
```

## Fixing it

Write the type in front of it, and drop the `using` lines it no longer
needs. `Integer.parse` gives a `Result`, so `.or` supplies a number for
text that does not parse:

```kex
main do
  let year = Integer.parse("2024").or(0)
  IO.printLine(year + 1)
end
```

A `parse` you declare yourself, with the same number of arguments, is used
instead of the imported ones, so the call is no longer ambiguous. The two
`using` lines are still rejected, though: keep only the one you need.
