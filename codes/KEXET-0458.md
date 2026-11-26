---
title: KEXET-0458
---

The part before `then` has to be a `Bool`, and `items.count` is an
`Integer`.

```kex
main do
  let items = [1, 2]
  IO.printLine(items.count then "some" else "none")
end
```

```
example.kex:3:28: [KEXET-0458]: Error, then/else condition must be Bool, got Integer
  |
3 |   IO.printLine(items.count then "some" else "none")
  |                ^^^^^^^^^^^
```

In an `if`, the same mistake is [KEXET-0443](../KEXET-0443/).

## Fixing it

Ask a question that answers `Bool`:

```kex
main do
  let items = [1, 2]
  IO.printLine(items.empty? then "none" else "some")
end
```
