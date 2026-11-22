---
title: KEXET-0124
---

`label` says it returns a `String`, but this `return` gives back an
`Integer`.

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

If the last expression of the body has the wrong type, the error is
[KEXET-0127](../KEXET-0127/).

## Fixing it

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
