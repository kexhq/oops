---
title: KEXET-0430
---

`Integer.parse` gives a `Result`, and `.or` is what takes the number out
of it. The fallback has to be a plain `Integer`, and `Ok(0)` is still a
`Result`.

```kex
main do
  let count = Integer.parse("4").or(Ok(0))
  IO.printLine(count)
end
```

```
example.kex:2:37: [KEXET-0430]: Error, `or` needs a fallback of type Integer, but got `Ok(…)`. `or` is what leaves the result; pass a plain default, keep the value as it is, or `match` on it
  |
2 |   let count = Integer.parse("4").or(Ok(0))
  |                                     ^^^^^
```

For an optional, the same mistake is [KEXET-0429](../KEXET-0429/).

## Fixing it

Pass the plain value:

```kex
main do
  let count = Integer.parse("4").or(0)
  IO.printLine(count)
end
```
