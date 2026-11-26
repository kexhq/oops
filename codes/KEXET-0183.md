---
title: KEXET-0183
---

`User` already has a `name` field. The `name : String` line in the `make`
block does not repeat it: there it declares a function called `name`, and
nothing defines that function.

```kex
record User do
  name : String
end

make User do
  name : String

  let greeting = "Hello, ${@name}"
end
```

```
example.kex:6:3: [KEXET-0183]: Error, `name` is declared in this `make` block but nothing defines it. Inside a `make` block `name : …` declares a FUNCTION, not a record field; the field is already declared by `record User`, so drop this line
  |
6 |   name : String
  |   ^^^^^^^^^^^^^
```

## Fixing it

Delete the line. Fields are listed once, in the `record`, and `@name` reads
the field inside the `make` block:

```kex
record User do
  name : String
end

make User do
  let greeting = "Hello, ${@name}"
end

main do
  IO.printLine(User { name: "Ada" }.greeting)
end
```
