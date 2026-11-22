---
title: KEXEP-0078
---

The subject of a `match` is followed by `do`, as in `match n do`. Here the
line ends after `n`.

```kex
let name(n: Integer) -> String do
  match n
    1 => "one"
    _ => "many"
  end
end
```

```
example.kex:2:10: [KEXEP-0078]: Error, expected 'do' after match subject, got Newline
  |
2 |   match n
  |          ^
```

Ruby's `case n` ... `when 1` is written `match n do` ... `1 =>` in Kex.

## Fixing it

```kex
let name(n: Integer) -> String do
  match n do
    1 => "one"
    _ => "many"
  end
end

main do
  IO.printLine(name(1))
end
```
