---
title: KEXET-0184
---

`email : String` looks like a field, but a `make` block holds methods. Inside
it, `email : String` declares a method called `email`, and no `let email`
follows to define it.

```kex
record User do
  name : String
end

make User do
  email : String

  let greeting = "Hello, ${@name}"
end
```

```
example.kex:6:3: [KEXET-0184]: Error, `email` is declared in this `make` block but nothing defines it. Inside a `make` block `email : …` declares a METHOD, not a record field; declare fields in `record User`
  |
6 |   email : String
  |   ^^^^^^^^^^^^^^
```

If `User` already has a field with that name, the error is
[KEXET-0183](../KEXET-0183/) instead.

## Fixing it

Move the field into the record:

```kex
record User do
  name : String
  email : String
end

make User do
  let greeting = "Hello, ${@name}"
end

main do
  IO.printLine(User { name: "Ada", email: "ada@example.com" }.greeting)
end
```
