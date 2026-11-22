---
title: KEXET-0145
---

There is no type called `Str`. It is spelled `String`.

```kex
let greet(name: Str) -> String = "hello, ${name}"
```

```
example.kex:1:17: [KEXET-0145]: Error, unknown type `Str`
  |
1 | let greet(name: Str) -> String = "hello, ${name}"
  |                 ^^^
```

Calls to `greet` can fail as well, because their arguments are checked
against `Str`. Those errors go away once this one is fixed.

## Fixing it

```kex
let greet(name: String) -> String = "hello, ${name}"
```

`kex -s` lists the standard library's types. A type of your own has to be
defined or imported where you use it.
