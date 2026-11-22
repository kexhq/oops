---
title: KEXET-0409
---

`.try` works on a `Result` or an optional. `n` is a plain `Integer`, which
cannot fail, so there is nothing for `.try` to do.

```kex
let double(n: Integer) -> Integer? do
  let value = n.try
  value * 2
end

main do
  IO.printLine(double(4).or(0))
end
```

```
example.kex:2:20: [KEXET-0409]: Error, `.try` expects Result or Optional, got Integer
  |
2 |   let value = n.try
  |               ^^^^^
```

## Fixing it

Drop `.try`. With it gone, the function can return a plain `Integer`
too:

```kex
let double(n: Integer) -> Integer = n * 2

main do
  IO.printLine(double(4))
end
```
