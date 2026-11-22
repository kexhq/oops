---
title: KEXET-0454
---

The `age` field of `User` is an `Integer`, and `"36"` is a `String`.

```kex
record User do
  name : String
  age : Integer
end

main do
  let user = User { name: "Ada", age: "36" }
  IO.printLine(user.age)
end
```

```
example.kex:7:39: [KEXET-0454]: Error, `User.age` expects Integer, but got String
  |
7 |   let user = User { name: "Ada", age: "36" }
  |                                       ^^^^
```

## Fixing it

```kex
record User do
  name : String
  age : Integer
end

main do
  let user = User { name: "Ada", age: 36 }
  IO.printLine(user.age)
end
```

If the value comes from text, such as user input, convert it with
`.to(Integer)` first.
