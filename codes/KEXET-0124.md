---
title: KEXET-0124
---

A `return` gives back a different type from the one the function declares.
The message points at that `return`.

```kex
let label(n: Integer) -> String do
  if n < 0
    return n
  end
  "positive"
end

main do
  IO.printLine(label(-3))
end
```

```
example.kex:3:5: [KEXET-0124]: Error, `label` declared to return String but returns Integer here
  |
3 |     return n
  |     ^^^^^^^^
```

When it's the last expression of the body that has the wrong type, the
error is [KEXET-0127](../KEXET-0127/).

## Fixing it

Return a value of the declared type:

```kex
let label(n: Integer) -> String do
  if n < 0
    return "negative"
  end
  "positive"
end

main do
  IO.printLine(label(-3))
end
```
