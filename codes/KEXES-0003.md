---
title: KEXES-0003
---

`break` only works inside a `while` or a `loop`. Here there is no loop
at all.

```kex
let check(n: Integer) -> String do
  if n < 0
    break
  end
  "ok"
end
```

```
example.kex:3:5: [KEXES-0003]: Error, 'break' used outside a loop
  |
3 |     break
  |     ^^^^^
```

`break` inside a block, such as one passed to `each`, is
[KEXES-0002](../KEXES-0002/).

## Fixing it

To leave a function early, use `return`:

```kex
let check(n: Integer) -> String do
  if n < 0
    return "negative"
  end
  "ok"
end

main do
  IO.printLine(check(-1))
end
```
