---
title: KEXET-0499
---

`n` is an `Integer`, and the arm's pattern is a `String`. An arm whose
literal is of another type than the value being matched can never match,
so only the other arms would ever run.

```kex
let name(n: Integer) -> String do
  match n do
    "one" => "1"
    _ => "other"
  end
end

main do
  IO.printLine(name(1))
end
```

```
example.kex:3:5: [KEXET-0499]: Error, the pattern `"one"` never matches a value of type Integer
  |
3 |     "one" => "1"
  |     ^^^^^
```

An `Integer` literal matches an equal `Float` and the other way round. A
constructor of another type is [KEXET-0115](../KEXET-0115/).

## Fixing it

Write the pattern as a value of the matched type:

```kex
let name(n: Integer) -> String do
  match n do
    1 => "one"
    _ => "other"
  end
end

main do
  IO.printLine(name(1))
end
```
