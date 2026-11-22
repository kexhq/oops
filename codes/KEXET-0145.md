---
title: KEXET-0145
---

A type annotation names a type that doesn't exist. Usually it's a typo or a
type name from another language.

```kex
let greet(name: Str) -> String = "hello, ${name}"
```

```
example.kex:1:17: [KEXET-0145]: Error, unknown type `Str`
  |
1 | let greet(name: Str) -> String = "hello, ${name}"
  |                 ^^^
```

Calls to the function can then report more errors, because their arguments
are checked against the unknown type. Fix this one first.

## Fixing it

Use the type's real name:

```kex
let greet(name: String) -> String = "hello, ${name}"
```

Bare `kex -s` lists the standard library's types. If the type is your own,
check that it's defined, or imported from the module that defines it.
