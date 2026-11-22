---
title: KEXET-0486
---

Two functions called `sqrt` are in scope, one taking a `Number` and one
taking a `Float`. `16.0` fits both, and neither is a better match, so the
compiler will not pick one for you.

```kex
main do
  IO.printLine(sqrt(16.0))
end
```

```
example.kex:2:16: [KEXET-0486]: Error, ambiguous overload for `sqrt`; candidates:

sqrt : Number -> Float

sqrt : Float -> Float
  |
2 |   IO.printLine(sqrt(16.0))
  |                ^^^^^^^^^^
```

## Fixing it

Say which one you mean, by its module:

```kex
main do
  IO.printLine(Math.sqrt(16.0))
end
```

`16.0.sqrt` works too.
