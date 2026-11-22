---
title: KEXET-0423
---

The code calls `Module.name`, the module exists, but it has no function by
that name.

```kex
main do
  IO.beep
end
```

```
example.kex:2:10: [KEXET-0423]: Error, `IO` has no function `beep`
  |
2 |   IO.beep
  |   ^^^^^^^
```

When the module has a function with a similar name, you get
[KEXET-0424](../KEXET-0424/) instead, which suggests it. A module name
that doesn't exist at all is [KEXET-0421](../KEXET-0421/).

## Fixing it

List what the module offers, for example with `kex -s IO`, and call one of
those. If the function is in your own module, check that it's defined there
and spelled the same.
