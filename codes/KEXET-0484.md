---
title: KEXET-0484
---

`adder` takes no arguments and returns a function. Arguments after it go
to that function, so `adder(1, 2)` means `adder()(1, 2)`. The function
`adder` returns takes one number, not two.

```kex
let adder() -> (Integer -> Integer) = { |x| x + 10 }

main do
  IO.printLine(adder(1, 2))
end
```

```
example.kex:4:16: [KEXET-0484]: Error, `adder` takes no arguments; the function it returns expects 1 argument(s), got 2
  |
4 |   IO.printLine(adder(1, 2))
  |                ^^^^^^^^^^^
```

## Fixing it

Pass the one argument the returned function wants:

```kex
let adder() -> (Integer -> Integer) = { |x| x + 10 }

main do
  IO.printLine(adder(1))
end
```

If you wanted to add two numbers, `adder` is the wrong shape. Give it two
parameters: `let add(x: Integer, y: Integer) = x + y`.
