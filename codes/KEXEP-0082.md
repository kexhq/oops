---
title: KEXEP-0082
---

Each arm of a `match` is `pattern => result`, with `=>`. `->` is used
for function types, not here.

```kex
let name(n: Integer) -> String do
  match n do
    1 -> "one"
    _ -> "many"
  end
end
```

```
example.kex:3:7: [KEXEP-0082]: Error, expected '=>' in match clause, got ->
  |
3 |     1 -> "one"
  |       ^^
```

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
