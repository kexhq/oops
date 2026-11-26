---
title: KEXET-0486
---

There are two functions called `describe`, one for an `Integer` or a
`String` and one for an `Integer` or a `Bool`. `1` fits both, and neither
is a better match, so the compiler will not pick one for you.

```kex
let describe(value: Integer | String) = "a number or some text"
let describe(value: Integer | Bool) = "a number or a flag"

main do
  IO.printLine(describe(1))
end
```

```
example.kex:5:16: [KEXET-0486]: Error, ambiguous overload for `describe`; candidates:

describe : Integer | String -> String

describe : Integer | Bool -> String
  |
5 |   IO.printLine(describe(1))
  |                ^^^^^^^^^^^
```

## Fixing it

Give each type exactly one overload, so that any argument matches only
one of them:

```kex
let describe(value: Integer) = "a number"
let describe(value: String) = "some text"
let describe(value: Bool) = "a flag"

main do
  IO.printLine(describe(1))
end
```
