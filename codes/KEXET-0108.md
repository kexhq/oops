---
title: KEXET-0108
---

The `match` handles `1` and `2`, but `n` can be any `Integer`. The compiler
wants every value covered, so that no call can fall through.

```kex
let name(n: Integer) -> String do
  match n do
    1 => "one"
    2 => "two"
  end
end

main do
  IO.printLine(name(3))
end
```

```
example.kex:2:3: [KEXET-0108]: Error, non-exhaustive match: missing case(s) _
  |
2 |   match n do
  |   ^^^^^^^^^^
```

`_` in the message means "everything else". For a sum type with a missing
constructor, the error is [KEXET-0107](../KEXET-0107/).

## Fixing it

Add an arm for the rest:

```kex
let name(n: Integer) -> String do
  match n do
    1 => "one"
    2 => "two"
    _ => "many"
  end
end

main do
  IO.printLine(name(3))
end
```
