---
title: KEXET-0460
---

There are two functions called `label`, one for an `Integer` and one for
a `String`. `~label` takes one of them as a value, but nothing here says
which.

```kex
let label(n: Integer) = "#${n}"
let label(s: String) = s

main do
  let show = ~label
  IO.printLine(show(3))
end
```

```
example.kex:5:14: [KEXET-0460]: Error, cannot reference overloaded function `label` without disambiguating arguments

label : Integer -> String

label : String -> String
  |
5 |   let show = ~label
  |              ^^^^^^
```

## Fixing it

Wrap the call in a block. The argument then picks the overload each time
`show` is called:

```kex
let label(n: Integer) = "#${n}"
let label(s: String) = s

main do
  let show = { |n| label(n) }
  IO.printLine(show(3))
end
```

When `~label` is passed straight to a function that knows the argument
type, it is fine as it is: in `[1, 2].map(~label)` the list says
`Integer`.
