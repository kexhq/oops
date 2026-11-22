---
title: KEXET-0451
---

`...admin` copies the fields of another record into the new one, but only
from a record of the same type. `admin` is an `Admin`, not a `User`, even
though both have a `name`.

```kex
record Admin do
  name : String
end

record User do
  name : String
end

main do
  let admin = Admin { name: "Ada" }
  let user = User { ...admin }
  IO.printLine(user.name)
end
```

```
example.kex:11:24: [KEXET-0451]: Error, record spread expects `User`, but got Admin
   |
11 |   let user = User { ...admin }
   |                        ^^^^^
```

## Fixing it

Name the fields you want to carry over:

```kex
record Admin do
  name : String
end

record User do
  name : String
end

main do
  let admin = Admin { name: "Ada" }
  let user = User { name: admin.name }
  IO.printLine(user.name)
end
```

A spread works when the types agree, as in `User { ...user, name: "Grace" }`.
