---
title: KEXET-0447
---

`after timeout:` waits a number of milliseconds, written as a plain
`Integer`. `5.second` is a `Measure<Quantity.Time>`, a span of time with its
unit attached, so `receive` cannot use it as it is.

```kex
foul waitForJob() do
  receive do
    job: String => IO.printLine("got ${job}")
  after timeout: 5.second
    IO.printLine("no job in 5 seconds")
  end
end
```

```
example.kex:4:26: [KEXET-0447]: Error, `after timeout:` takes milliseconds, an Integer, but got Measure<Quantity.Time>
  |
4 |   after timeout: 5.second
  |                  ^^^^^^^^
```

## Fixing it

Turn the span into whole milliseconds:

```kex
foul waitForJob() do
  receive do
    job: String => IO.printLine("got ${job}")
  after timeout: 5.second.wholeMilliseconds
    IO.printLine("no job in 5 seconds")
  end
end
```

Or write the number itself, `after timeout: 5000`.
