---
title: KEXEF-0003
---

`~IO.printLine` passes `IO.printLine` along as a value, and `each` calls it
for every line. `report` is a plain `let`, so it cannot hand on a `foul`
function any more than it can call one.

```kex
let report(lines: [String]) -> [String] do
  lines.each(~IO.printLine)
  lines
end
```

```
example.kex:2:14: [KEXEF-0003]: Error, cannot capture foul function 'IO.printLine' from pure context
  |
2 |   lines.each(~IO.printLine)
  |              ^^^^^^^^^^^^^
```

Calling a `foul` function directly from pure code is
[KEXEF-0001](../KEXEF-0001/).

## Fixing it

Mark `report` as `foul`:

```kex
foul report(lines: [String]) -> [String] do
  lines.each(~IO.printLine)
  lines
end

main do
  report(["one", "two"])
end
```

Or keep `report` pure and print the lines where it is called, in `main` or
another `foul` function.
