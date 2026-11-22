---
title: KEXET-0110
---

`Result` takes two types: the value when it works, and the error when it
does not. `describe` names only the first.

```kex
let describe(port: Result<Integer>) -> String = "port"
```

```
example.kex:1:20: [KEXET-0110]: Error, `Result` takes 2 type arguments, but 1 is given
  |
1 | let describe(port: Result<Integer>) -> String = "port"
  |                    ^^^^^^^^^^^^^^^
```

`Map` is the same: it needs a key type and a value type, as in
`Map<String, Integer>`.

## Fixing it

Name the error type too. For a port read with `Integer.parse`, that is
`ParseError`:

```kex
let describe(port: Result<Integer, ParseError>) -> String = "port"
```

If the error does not matter, `Integer?` may be the better type.
