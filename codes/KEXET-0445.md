---
title: KEXET-0445
---

An `if` with an `else` is a value, so both branches must have the same
type. The first branch gives a `String`, and the `else` gives `n`, an
`Integer`.

```kex
let describe(n: Integer) -> String do
  if n > 0
    "positive"
  else
    n
  end
end

main do
  IO.printLine(describe(4))
end
```

```
example.kex:2:3: [KEXET-0445]: Error, branch type mismatch: 'if' returns String but 'else' returns Integer
  |
2 |   if n > 0
  |   ^^^^^^^^
```

The same mistake with `then ... else` is [KEXET-0459](../KEXET-0459/).

## Fixing it

Make the `else` give a `String` too:

```kex
let describe(n: Integer) -> String do
  if n > 0
    "positive"
  else
    "${n}"
  end
end

main do
  IO.printLine(describe(4))
end
```
