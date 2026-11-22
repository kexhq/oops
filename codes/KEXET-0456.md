---
title: KEXET-0456
---

`User` has three fields with no default, and this `User` was made with only
`name`. The message lists every field that is missing.

```kex
record User do
  name : String
  age : Integer
  email : String
end

main do
  let user = User { name: "Ada" }
  IO.printLine(user.name)
end
```

```
example.kex:8:14: [KEXET-0456]: Error, missing mandatory fields `age`, `email` constructing `User`
  |
8 |   let user = User { name: "Ada" }
  |              ^^^^^^^^^^^^^^^^^^^^
```

With one field missing, the error is [KEXET-0455](../KEXET-0455/).

## Fixing it

Give every field a value:

```kex
record User do
  name : String
  age : Integer
  email : String
end

main do
  let user = User { name: "Ada", age: 36, email: "ada@example.com" }
  IO.printLine(user.name)
end
```

A field that most users share a value for can have a default in the record,
such as `age : Integer = 0`, and can then be left out.
