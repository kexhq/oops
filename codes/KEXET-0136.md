---
title: KEXET-0136
---

Inside `make Timer`, `tick()` calls the block's own `tick` on the current
timer. `tick` takes one argument, `by`, and this call passes none.

```kex
record Timer do
  seconds : Integer
end

make Timer do
  let tick(by: Integer) = Timer { seconds: @seconds - by }
  let done() = tick()
end

main do
  IO.printLine(Timer { seconds: 5 }.done.seconds)
end
```

```
example.kex:7:16: [KEXET-0136]: Error, `tick` expects 1 argument(s), got 0
  |
7 |   let done() = tick()
  |                ^^^^^^
```

## Fixing it

Pass the argument:

```kex
record Timer do
  seconds : Integer
end

make Timer do
  let tick(by: Integer) = Timer { seconds: @seconds - by }
  let done() = tick(@seconds)
end

main do
  IO.printLine(Timer { seconds: 5 }.done.seconds)
end
```

Written out as `this.tick()`, the call counts the timer as an argument
too, so the same mistake reads as
[KEXET-0472](../KEXET-0472/).
