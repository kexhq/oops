---
title: KEXET-0452
---

`User` has no field called `age`. The message lists the fields it does
have, here only `name`.

```kex
record User do
  name : String
end

main do
  let user = User { name: "Ada", age: 36 }
  IO.printLine(user.name)
end
```

```
example.kex:6:39: [KEXET-0452]: Error, record `User` has no field `age`. It has name
  |
6 |   let user = User { name: "Ada", age: 36 }
  |                                       ^^
```

## Fixing it

If the field name is a typo, use one from the list. If `User` should have
an `age`, add it to the record:

```kex
record User do
  name : String
  age : Integer
end

main do
  let user = User { name: "Ada", age: 36 }
  IO.printLine(user.name)
end
```
