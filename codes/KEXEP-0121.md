---
title: KEXEP-0121
---

A map entry is `key: value`. `"alan" => 41` is Ruby's form, and the
parser stops at the `=>`.

```kex
main do
  let ages = { "ada": 36, "alan" => 41 }
  IO.printLine(ages)
end
```

```
example.kex:2:34: [KEXEP-0121]: Error, expected ':' in map entry, got =>
  |
2 |   let ages = { "ada": 36, "alan" => 41 }
  |                                  ^^
```

When the very first entry uses `=>`, the error is the general
[KEXEP-0074](../KEXEP-0074/) instead.

## Fixing it

```kex
main do
  let ages = { "ada": 36, "alan": 41 }
  IO.printLine(ages)
end
```
