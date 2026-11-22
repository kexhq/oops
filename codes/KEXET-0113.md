---
title: KEXET-0113
---

`Light` belongs to `Shade`, but `color` is a `Color`. A `Color` can never
be `Light`, so this arm would never run.

```kex
type Color = Red | Blue
type Shade = Light | Dark

let describe(color: Color) -> String do
  match color do
    Light => "light"
    _ => "dark"
  end
end

main do
  IO.printLine(describe(Red))
end
```

```
example.kex:6:5: [KEXET-0113]: Error, `Light` is a constructor of `Shade`, but the value being matched has type `Color`. This pattern can never match
  |
6 |     Light => "light"
  |     ^^^^^
```

## Fixing it

Match on the constructors of the type you have:

```kex
match color do
  Red => "red"
  Blue => "blue"
end
```

If you meant to match on a `Shade`, the mistake is in the value passed to
`match`.
