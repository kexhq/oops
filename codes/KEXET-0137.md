---
title: KEXET-0137
---

Inside `make Clock`, `later` has two forms: one with no arguments and one
with one. `later(1, 2)` passes two, which neither form takes.

```kex
record Clock do
  minutes : Integer
end

make Clock do
  let later -> This = later(1)
  let later(by: Integer) -> This = New { minutes: @minutes + by }
  let muchLater -> This = later(1, 2)
end
```

```
example.kex:8:27: [KEXET-0137]: Error, `later` expects one of these argument counts: 0, 1 (got 2)
  |
8 |   let muchLater -> This = later(1, 2)
  |                           ^^^^^^^^^^^
```

With only one form, the error is [KEXET-0136](../KEXET-0136/), which gives
the single count.

## Fixing it

Call one of the forms that exist:

```kex
record Clock do
  minutes : Integer
end

make Clock do
  let later -> This = later(1)
  let later(by: Integer) -> This = New { minutes: @minutes + by }
  let muchLater -> This = later(60)
end

main do
  IO.printLine(Clock { minutes: 0 }.muchLater.minutes)
end
```
