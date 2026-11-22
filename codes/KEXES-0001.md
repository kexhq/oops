---
title: KEXES-0001
---

There are two records called `User`. A record is defined once, with all
of its fields.

```kex
record User do
  name : String
end

record User do
  email : String
end
```

```
example.kex:5:1: [KEXES-0001]: Error, duplicate record definition: User
  |
5 | record User do
  | ^^^^^^^^^^^^^^
```

## Fixing it

Put the fields together in one record:

```kex
record User do
  name : String
  email : String
end

main do
  IO.printLine(User { name: "Ada", email: "ada@example.com" }.email)
end
```

If they really are two different things, give them two names.
