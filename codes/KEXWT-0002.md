---
title: KEXWT-0002
---

`people` is bound to `0`, so `12 / people` divides by zero every time it
runs. This is a warning, so the program still compiles, but it stops with
a runtime error when it reaches the division. `%`, `div`, `modulo` and
`divmod` are warned about the same way.

```kex
main do
  let people = 0
  IO.printLine(12 / people)
end
```

```
example.kex:3:21: [KEXWT-0002]: Warning, division by zero: the divisor of `/` is always 0, so this fails at run time
  |
3 |   IO.printLine(12 / people)
  |                ^^^^^^^^^^^
```

## Fixing it

Divide by the number you meant. When the divisor can really be zero, say
what happens then before dividing:

```kex
let share(total: Integer, people: Integer) -> Integer? do
  return None if people == 0
  Just(total / people)
end

main do
  IO.printLine(share(12, 0).or(0))
end
```
