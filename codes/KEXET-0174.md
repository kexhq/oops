---
title: KEXET-0174
---

`Type.returnedBy` is worked out by the compiler, from the signature of
the function it is given. `~area` is a function value, and a value
carries no signature.

```kex
let area(w: Integer, h: Integer) -> Integer = w * h

type Area = Type.returnedBy(~area)
```

```
example.kex:3:29: [KEXET-0174]: Error, `Type.returnedBy` needs the NAME of a function; a lambda or a function value carries no signature
  |
3 | type Area = Type.returnedBy(~area)
  |                             ^^^^^
```

A block such as `{ |w, h| area(w, h) }` gives the same error.

## Fixing it

Write the bare name, without `~`:

```kex
let area(w: Integer, h: Integer) -> Integer = w * h

type Area = Type.returnedBy(area)

main do
  let room: Area = area(3, 4)
  IO.printLine(room)
end
```
