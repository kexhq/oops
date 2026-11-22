---
title: KEXET-0446
---

Every arm of a `match` gives the result of the whole `match`, so they must
all have the same type. The first arms give a `String`, and the last gives
`n`, an `Integer`.

```kex
let name(n: Integer) -> String do
  match n do
    1 => "one"
    2 => "two"
    _ => n
  end
end

main do
  IO.printLine(name(3))
end
```

```
example.kex:2:3: [KEXET-0446]: Error, match arm type mismatch: expected String but arm returns Integer
  |
2 |   match n do
  |   ^^^^^^^^^^
```

## Fixing it

```kex
let name(n: Integer) -> String do
  match n do
    1 => "one"
    2 => "two"
    _ => "${n}"
  end
end

main do
  IO.printLine(name(3))
end
```
