---
title: KEXEP-0062
---

After `retries:` comes the type of the parameter. `3` is a value, not a
type.

```kex
let connect(retries: 3) = "trying ${retries} times"

main do
  IO.printLine(connect(5))
end
```

```
example.kex:1:22: [KEXEP-0062]: Error, expected type expression
  |
1 | let connect(retries: 3) = "trying ${retries} times"
  |                      ^
example.kex:4:16: [KEXET-0163]: Error, undefined function: `connect`
  |
4 |   IO.printLine(connect(5))
  |                ^^^^^^^^^^
```

`connect` could not be read, so it was never defined. That is why the
call to it is an error too. It goes away with the first one.

## Fixing it

To give `retries` a default, write the type and then `= 3`:

```kex
let connect(retries: Integer = 3) = "trying ${retries} times"

main do
  IO.printLine(connect())
  IO.printLine(connect(5))
end
```
