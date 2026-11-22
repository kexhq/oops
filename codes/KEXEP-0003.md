---
title: KEXEP-0003
---

Outside of any function, the parser found something that cannot start a
definition. Most often it is an `end` too many, like the one on line 4.

```kex
let double(n: Integer) -> Integer do
  n * 2
end
end

main do
  IO.printLine(double(4))
end
```

```
example.kex:4:1: [KEXEP-0003]: Error, unexpected token at top level: end
  |
4 | end
  | ^^^
```

Ruby's `def` ends up here too: Kex reads `def` as a name, and the parser
then trips over the `end` that closes it. Functions are written with `let`
or `foul`.

## Fixing it

Remove the extra `end`:

```kex
let double(n: Integer) -> Integer do
  n * 2
end

main do
  IO.printLine(double(4))
end
```
