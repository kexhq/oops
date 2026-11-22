---
title: KEXEM-0008
---

`except:` leaves names out of an import, and `square` is never imported
anyway, because it is private. Naming it here is an error, even though
leaving it out is what you want.

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

using Geometry, except: [square]

main do
  IO.printLine(area(3.0))
end
```

```
example.kex:9:1: [KEXEM-0008]: Error, cannot reference private name `square` from Geometry
  |
9 | using Geometry, except: [square]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Drop it from the list. If nothing else is left out, drop `except:` too:

```kex
module Geometry do
  let area(r: Float) -> Float = Math.PI * square(r)

  private do
    let square(n: Float) -> Float = n * n
  end
end

using Geometry

main do
  IO.printLine(area(3.0))
end
```
