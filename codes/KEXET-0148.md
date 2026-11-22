---
title: KEXET-0148
---

`limit` is defined in the `Config` module, and this code is outside it.
From outside, a module's names are reached through the module, or brought
in with `using`.

```kex
module Config do
  let limit = 10
end

main do
  IO.printLine(limit)
end
```

```
example.kex:6:16: [KEXET-0148]: Error, undefined name: `limit`. `Config.limit` is not imported here
  |
6 |   IO.printLine(limit)
  |                ^^^^^
```

For a function, the same error is [KEXET-0165](../KEXET-0165/).

## Fixing it

```kex
module Config do
  let limit = 10
end

main do
  IO.printLine(Config.limit)
end
```

Or put `using Config` above `main`, and keep writing `limit`.
