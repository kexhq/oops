---
title: KEXET-0449
---

`New { ... }` copies "this value" with some fields changed, and there is
only a "this value" inside a function in a `make` block. `rename` is an
ordinary function.

```kex
record User do
  name : String
end

let rename(user: User, name: String) -> User = New { name: name }
```

```
example.kex:5:48: [KEXET-0449]: Error, `New` construction requires a make block receiver
  |
5 | let rename(user: User, name: String) -> User = New { name: name }
  |                                                ^^^^^^^^^^^^^^^^^^
```

## Fixing it

Outside a `make` block, copy the record by name, with `...` for the fields
that stay the same:

```kex
record User do
  name : String
end

let rename(user: User, name: String) -> User = User { ...user, name: name }

main do
  IO.printLine(rename(User { name: "Ada" }, "Grace").name)
end
```

Or move `rename` into a `make User` block, where `New { name: name }`
works.
