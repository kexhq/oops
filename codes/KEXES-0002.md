---
title: KEXES-0002
---

`break` leaves a `while` or `loop`. The block passed to `each` is a
function of its own, so there is no loop inside it for `break` to leave.

```kex
main do
  [1, 2, 3].each do |n|
    break if n > 1
    IO.printLine(n)
  end
end
```

```
example.kex:3:5: [KEXES-0002]: Error, 'break' cannot be used inside a closure
  |
3 |     break if n > 1
  |     ^^^^^
```

## Fixing it

Take only the elements you want before going over them:

```kex
main do
  [1, 2, 3].takeWhile { |n| n <= 1 }.each do |n|
    IO.printLine(n)
  end
end
```

`while` and `loop do` take `break` and `next`, if you need a loop
you can stop.
