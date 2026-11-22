---
title: KEXET-0140
---

`Metric` and `Imperial` both have a `distance`. After both `using` lines, a
bare `distance` could mean either one, so the second `using` is rejected.
This happens even if `distance` is never called.

```kex
module Metric do
  let distance(km: Float) -> String = "${km} km"
end

module Imperial do
  let distance(km: Float) -> String = "${km * 0.621} mi"
end

using Metric
using Imperial

main do
  IO.printLine(distance(5.0))
end
```

```
example.kex:10:1: [KEXET-0140]: Error, ambiguous name `distance`, imported from both `Metric` and `Imperial`
   |
10 | using Imperial
   | ^^^^^^^^^^^^^^
```

## Fixing it

Import one of them, and call the other by its module name:

```kex
module Metric do
  let distance(km: Float) -> String = "${km} km"
end

module Imperial do
  let distance(km: Float) -> String = "${km * 0.621} mi"
end

using Metric

main do
  IO.printLine(distance(5.0))
  IO.printLine(Imperial.distance(5.0))
end
```

An `only:` list that leaves `distance` out of one of the imports works too.
