---
title: KEXET-0443
---

An `if` needs a `Bool`, and `first` is a `String?`. Kex has no `nil`, and
it does not treat a missing value as false the way Ruby does.

```kex
main do
  let first = ["ada", "alan"].first
  if first
    IO.printLine(first)
  end
end
```

```
example.kex:3:6: [KEXET-0443]: Error, if condition must be Bool, got String?
  |
3 |   if first
  |      ^^^^^
```

## Fixing it

Use `if let` to take the value out when there is one:

```kex
main do
  let first = ["ada", "alan"].first
  if let Just(name) = first
    IO.printLine(name)
  end
end
```

If you only need to know whether it is there, ask with `first.set?`.
