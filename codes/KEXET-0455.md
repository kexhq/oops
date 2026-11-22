---
title: KEXET-0455
---

`User` has an `age` field with no default, so every `User` needs one, and
this one was made without it.

```kex
record User do
  name : String
  age : Integer
end

main do
  let user = User { name: "Ada" }
  IO.printLine(user.name)
end
```

```
example.kex:7:14: [KEXET-0455]: Error, missing mandatory field `age` constructing `User`
  |
7 |   let user = User { name: "Ada" }
  |              ^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Give the field a value:

```kex
let user = User { name: "Ada", age: 36 }
```

Or, if most users can start with the same value, give the field a default
in the record, `age : Integer = 0`. Then it can be left out.
