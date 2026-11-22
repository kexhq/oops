---
title: KEXET-0457
---

There is no record called `Person`. The record defined here is `User`.

```kex
record User do
  name : String
end

main do
  let user = Person { name: "Ada" }
  IO.printLine(user.name)
end
```

```
example.kex:6:14: [KEXET-0457]: Error, unknown record type `Person`
  |
6 |   let user = Person { name: "Ada" }
  |              ^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

```kex
record User do
  name : String
end

main do
  let user = User { name: "Ada" }
  IO.printLine(user.name)
end
```

If `Person` is defined in another module, import that module.
