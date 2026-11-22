---
title: KEXET-0182
---

`shout : String -> String` declares a method in the `make User` block, but
there is no `let shout` to go with it.

```kex
record User do
  name : String
end

make User do
  shout : String -> String

  let greeting = "Hello, ${@name}"
end
```

```
example.kex:6:3: [KEXET-0182]: Error, `shout` is declared in this `make` block but nothing defines it. A method the runtime provides is declared with `:>`, which makes the receiver implicit
  |
6 |   shout : String -> String
  |   ^^^^^^^^^^^^^^^^^^^^^^^^
```

The second half of the message is for the standard library, where a few
methods have no Kex body and are written as `name :> type`. In your own
code you want the first half: write the method.

## Fixing it

Define `shout` under its signature:

```kex
record User do
  name : String
end

make User do
  shout : String -> String
  let shout(text) = "${text.upperCase}, ${@name}!"
end

main do
  IO.printLine(User { name: "Ada" }.shout("hello"))
end
```

If you did not mean to have a `shout` method at all, delete the line.
