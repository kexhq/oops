---
title: KEXET-0461
---

`@name` means "the `name` field of this value", and there is only a
"this value" inside a function in a `make` block. `greet` is an ordinary
function, so it has to name the user it was given.

```kex
record User do
  name : String
end

let greet(user: User) -> String = "hello, ${@name}"

main do
  IO.printLine(greet(User { name: "Ada" }))
end
```

```
example.kex:5:45: [KEXET-0461]: Error, 'this' has no receiver here: it is only bound inside a `make` block method
  |
5 | let greet(user: User) -> String = "hello, ${@name}"
  |                                             ^
```

## Fixing it

```kex
record User do
  name : String
end

let greet(user: User) -> String = "hello, ${user.name}"

main do
  IO.printLine(greet(User { name: "Ada" }))
end
```
