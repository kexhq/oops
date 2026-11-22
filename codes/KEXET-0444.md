---
title: KEXET-0444
---

Every branch of an `if` gives the value of the whole `if`, so they must
all have the same type. The `if` branch gives a `String`, and the `elif`
gives `80`, an `Integer`.

```kex
let grade(score: Integer) -> String do
  if score >= 90
    "A"
  elif score >= 80
    80
  else
    "C"
  end
end
```

```
example.kex:2:3: [KEXET-0444]: Error, branch type mismatch: 'if' returns String but 'elif' returns Integer
  |
2 |   if score >= 90
  |   ^^^^^^^^^^^^^^
```

The same mistake in the `else` branch is [KEXET-0445](../KEXET-0445/).

## Fixing it

```kex
let grade(score: Integer) -> String do
  if score >= 90
    "A"
  elif score >= 80
    "B"
  else
    "C"
  end
end

main do
  IO.printLine(grade(85))
end
```
