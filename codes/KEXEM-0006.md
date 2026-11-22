---
title: KEXEM-0006
---

Everything in `Helpers` is inside `private do`, so `export Helpers` would
give `Shop` nothing to pass on.

```kex
module Helpers do
  private do
    let tidy(name: String) -> String = name.trim
  end
end

module Shop do
  export Helpers
end

main do
  IO.printLine("ready")
end
```

```
example.kex:8:3: [KEXEM-0006]: Error, module Helpers has no public names to export
  |
8 |   export Helpers
  |   ^^^^^^^^^^^^^^
```

## Fixing it

If `tidy` is meant to be used from outside, make it public:

```kex
module Helpers do
  let tidy(name: String) -> String = name.trim
end

module Shop do
  export Helpers
end

main do
  IO.printLine(Shop.Helpers.tidy("  ada "))
end
```

If it is not, the `export` line is not needed at all.
