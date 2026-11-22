---
title: KEXET-0413
---

`user.name = ...` changes a field of a record held in a `var`. `user` is a
`User?` here, because `first` gives an optional, and an optional has no
fields to assign.

```kex
record User do
  name : String
end

main do
  var user = [User { name: "Ada" }].first
  user.name = "Grace"
  IO.printLine(user)
end
```

```
example.kex:7:3: [KEXET-0413]: Error, field assignment requires a record binding
  |
7 |   user.name = "Grace"
  |   ^^^^^^^^^^^^^^^^^^^
```

Assigning to a `let`, field or not, is [KEXET-0411](../KEXET-0411/).

## Fixing it

Take the `User` out of the optional first, so the `var` holds a record:

```kex
record User do
  name : String
end

main do
  var user = [User { name: "Ada" }].first.or(User { name: "nobody" })
  user.name = "Grace"
  IO.printLine(user.name)
end
```
