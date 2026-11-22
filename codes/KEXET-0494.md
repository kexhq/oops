---
title: KEXET-0494
---

`first` is a `String?`, and `"ada"` is a `String`. A value that might be
missing is never equal to a plain one, so this comparison would always be
`false`.

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first == "ada")
end
```

```
example.kex:3:25: [KEXET-0494]: Error, `String?` and `String` are never equal: compare with `Just(value)`, or unwrap first (`.or(default)`, a `match`)
  |
3 |   IO.printLine(first == "ada")
  |                ^^^^^^^^^^^^^^
```

## Fixing it

Compare it with an optional, `Just("ada")`:

```kex
main do
  let first = ["ada", "alan"].first
  IO.printLine(first == Just("ada"))
end
```

Or take the value out first, as in `first.or("") == "ada"`.
