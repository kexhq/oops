---
title: KEXEP-0081
---

The `match` was never closed. The file ends after its last arm, and the
parser is still waiting for `end`.

```kex
let name(n: Integer) -> String = match n do
  1 => "one"
  _ => "many"
```

```
example.kex:3:14: [KEXEP-0081]: Error, expected 'end' to close match, got Eof
  |
3 |   _ => "many"
  |              ^
```

A `match` written after `=` on one line still needs an `end` of its own
when its arms go on the following lines.

## Fixing it

```kex
let name(n: Integer) -> String = match n do
  1 => "one"
  _ => "many"
end

main do
  IO.printLine(name(1))
end
```
