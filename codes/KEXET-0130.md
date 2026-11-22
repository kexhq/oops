---
title: KEXET-0130
---

There is no trait called `Printable`. The trait named after `implement:`
has to be defined in this program or imported.

```kex
record User do
  name : String
end

make User, implement: Printable do
  let label -> String = @name
end
```

```
example.kex:5:1: [KEXET-0130]: Error, unknown trait: Printable
  |
5 | make User, implement: Printable do
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Define the trait, or import the module that has it:

```kex
trait Printable do
  label :> String
end

record User do
  name : String
end

make User, implement: Printable do
  let label -> String = @name
end

main do
  IO.printLine(User { name: "Ada" }.label)
end
```

If you meant one of the standard library's traits, `kex -s` lists them.
