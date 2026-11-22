---
title: KEXEP-0090
---

The wait in an `after` clause is always written with `timeout:` in front of
it. A bare `5000` is not enough.

```kex
foul nextJob() do
  receive do
    job: String => IO.printLine("working on ${job}")
  after 5000
    IO.printLine("no job came in")
  end
end
```

```
example.kex:4:9: [KEXEP-0090]: Error, expected 'timeout:' after 'after', got Integer [5000]
  |
4 |   after 5000
  |         ^^^^
```

The same error appears for an `after` with nothing after it, since a wait
with no time set could never end.

## Fixing it

```kex
foul nextJob() do
  receive do
    job: String => IO.printLine("working on ${job}")
  after timeout: 5000
    IO.printLine("no job came in")
  end
end
```
