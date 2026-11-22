---
title: KEXEP-0044
---

The parameter list opened after `add` is never closed: `b: Integer` has no
`)` after it. The parser reads on to the end of the line looking for one,
so the caret is there, and not where the `)` is missing.

```kex
let add(a: Integer, b: Integer -> Integer = a + b
```

```
example.kex:1:50: [KEXEP-0044]: Error, expected ')' after parameters, got Eof
  |
1 | let add(a: Integer, b: Integer -> Integer = a + b
  |                                                  ^
```

## Fixing it

Close the list before the return type:

```kex
let add(a: Integer, b: Integer) -> Integer = a + b

main do
  IO.printLine(add(1, 2))
end
```
