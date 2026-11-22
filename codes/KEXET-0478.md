---
title: KEXET-0478
---

`users.first` is a `User?`, because the list could be empty, and only a
`User` has a `name`. The message suggests mapping over the optional.

```kex
record User do
  name : String
end

main do
  let users = [User { name: "Ada" }]
  IO.printLine(users.first.name)
end
```

```
example.kex:7:32: [KEXET-0478]: Error, `name` is a field of User, but the receiver is User?. The value may be None. Map over the optional first: `.map { |v| v.name }`
  |
7 |   IO.printLine(users.first.name)
  |                ^^^^^^^^^^^^^^^^
example.kex:7:32: [KEXET-0491]: Error, `name` expects argument 1 to be Weekday, but got User?

name : Weekday -> String
  |
7 |   IO.printLine(users.first.name)
  |                ^^^^^^^^^^^^^^^^
```

## Fixing it

`map` reads the field when there is a user. `.or` gives a value for
the empty case:

```kex
record User do
  name : String
end

main do
  let users = [User { name: "Ada" }]
  IO.printLine(users.first.map { |user| user.name }.or("nobody"))
end
```

To handle the empty case with its own code, use
`if let Just(user) = users.first`.
