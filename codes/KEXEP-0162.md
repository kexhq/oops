---
title: KEXEP-0162
---

`when` guards an arm of a `match`, not a clause of a function. Elixir and
Haskell write `sign(n) when n < 0` to pick a clause; Kex picks a clause by
its parameter's pattern alone.

```kex
let sign(n: Integer) -> String when n < 0 = "negative"
let sign(_) -> String = "not negative"

main do
  IO.printLine(sign(-3))
end
```

```
example.kex:1:32: [KEXEP-0162]: Error, a function clause cannot have a `when` guard: match on the parameter in the body instead
  |
1 | let sign(n: Integer) -> String when n < 0 = "negative"
  |                                ^^^^
```

## Fixing it

Write one function, and move the guard into a `match` in its body:

```kex
let sign(n: Integer) -> String do
  match n do
    n when n < 0 => "negative"
    _ => "not negative"
  end
end

main do
  IO.printLine(sign(-3))
end
```

With only two cases, `n < 0 then "negative" else "not negative"` says the
same in one line.
