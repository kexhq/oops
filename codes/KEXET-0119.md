---
title: KEXET-0119
---

`half` returns an `Integer?`, which is either `Just` a number or `None`.
`Ok` is for a `Result`, so it can never match what `half` gives back.

```kex
let half(n: Integer) -> Integer? = n % 2 == 0 then Just(n / 2) else None

main do
  let Ok(h) = half(10)
  IO.printLine(h)
end
```

```
example.kex:4:7: [KEXET-0119]: Error, cannot match `Ok`: expected Result, got Integer?
  |
4 |   let Ok(h) = half(10)
  |       ^^^^^
```

## Fixing it

Use the constructors of an Optional. A `let` would fail at run time when
`half` gives `None`, so a `match` that covers both is safer:

```kex
let half(n: Integer) -> Integer? = n % 2 == 0 then Just(n / 2) else None

main do
  match half(10) do
    Just(h) => IO.printLine(h)
    None => IO.printLine("odd")
  end
end
```

Inside a `match`, the wrong constructor gives
[KEXET-0113](../KEXET-0113/) instead.
