---
title: KEXET-0185
---

In Ruby, `new` makes an object. In Kex, `new` is a name the compiler keeps
for itself: inside a `make` it is the copy of the receiver that is being
changed field by field. A function cannot be called `new`.

```kex
record User do
  name : String
end

make User do
  let new(name: String) -> This = User { name: name }
end
```

```
example.kex:6:3: [KEXET-0185]: Error, `new` is reserved for the next-state binding; use a name such as `build` for constructor functions
  |
6 |   let new(name: String) -> This = User { name: name }
  |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

A record is made with `User { ... }`, and a function that builds one can
have any other name. The message suggests `build`:

```kex
record User do
  name : String
end

let build(name: String) -> User = User { name: name.trim }

main do
  IO.printLine(build("  Ada ").name)
end
```
