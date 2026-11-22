---
title: KEXEP-0085
---

`receive` itself takes no options. How long it waits is set in its `after`
clause, which also says what to do when the time runs out.

```kex
foul nextJob() do
  receive timeout: 5000 do
    job: String => IO.printLine("working on ${job}")
  end
end
```

```
example.kex:2:11: [KEXEP-0085]: Error, the timeout belongs to the `after` clause: `receive do ... after timeout: 1000 ... end`
  |
2 |   receive timeout: 5000 do
  |           ^^^^^^^
```

## Fixing it

Move the timeout into an `after` clause at the end of the block:

```kex
foul nextJob() do
  receive do
    job: String => IO.printLine("working on ${job}")
  after timeout: 5000
    IO.printLine("no job came in")
  end
end
```
