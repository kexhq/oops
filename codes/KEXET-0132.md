---
title: KEXET-0132
---

`Clock` declares `now` as `foul`, because a real clock reads the time from
outside the program. `FixedClock` always gives the same time, so its `now`
was written with `let`. The trait still wants `foul`.

```kex
trait Clock do
  foul now :> Integer
end

record FixedClock do
  time : Integer
end

make FixedClock, implement: Clock do
  let now = @time
end
```

```
example.kex:9:1: [KEXET-0132]: Error, make FixedClock, implement: Clock. Method 'now' must be declared foul (trait requires it)
  |
9 | make FixedClock, implement: Clock do
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

Code that calls `now` on a `Clock` already treats it as foul, so the method
must be declared that way in every type that implements the trait.

## Fixing it

Write `foul` instead of `let`. The body can stay the same:

```kex
trait Clock do
  foul now :> Integer
end

record FixedClock do
  time : Integer
end

make FixedClock, implement: Clock do
  foul now = @time
end

main do
  IO.printLine(FixedClock { time: 1700000000 }.now)
end
```
