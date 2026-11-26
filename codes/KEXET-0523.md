---
title: KEXET-0523
---

`|(first, last)|` takes each element apart as a pair, but the elements of
`names` are single strings. A tuple pattern can only match a tuple, so
this one would never match anything.

```kex
main do
  let names = ["Ada", "Grace"]
  names.each do |(first, last)|
    IO.printLine("${first} ${last}")
  end
end
```

```
example.kex:3:18: [KEXET-0523]: Error, a tuple pattern never matches a value of type `String`
  |
3 |   names.each do |(first, last)|
  |                  ^^^^^^^^^^^^^
```

The same goes for `let (a, b) = n` when `n` is not a tuple.

## Fixing it

Give the block what the pattern expects, here a list of pairs:

```kex
main do
  let names = [("Ada", "Lovelace"), ("Grace", "Hopper")]
  names.each do |(first, last)|
    IO.printLine("${first} ${last}")
  end
end
```

If the elements really are single values, take each one with a plain
name, `|name|`.
