---
title: KEXET-0109
---

`Optional` takes one type: the type of the value that may be missing. A
missing value carries no reason, so there is no place for the `String`.

```kex
record User do
  name : String
end

let greet(user: Optional<User, String>) -> String = "Hello"
```

```
example.kex:5:17: [KEXET-0109]: Error, `Optional` takes 1 type argument, but 2 are given
  |
5 | let greet(user: Optional<User, String>) -> String = "Hello"
  |                 ^^^^^^^^^^^^^^^^^^^^^^
```

Too few type arguments, as in `Map<String>`, is
[KEXET-0110](../KEXET-0110/).

## Fixing it

If the `String` is the reason a user could not be found, the type you want
is `Result`, which takes a value type and an error type:

```kex
record User do
  name : String
end

let greet(user: Result<User, String>) -> String = "Hello"
```

If there is no reason to carry, drop the second type and write `User?`,
which is short for `Optional<User>`.
