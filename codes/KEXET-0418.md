---
title: KEXET-0418
---

`Column` defines `==` to build a `Filter`, not to answer true or false.
Kex can only make `!=` out of `==` by flipping a `Bool`, and a `Filter`
cannot be flipped.

```kex
type Filter = Equals(String, String)

record Column do
  name : String
end

make Column do
  let ==(value: String) -> Filter = Equals(@name, value)
end

main do
  let email = Column { name: "email" }
  IO.printLine(email != "ada@example.com")
end
```

```
example.kex:13:25: [KEXET-0418]: Error, `!=` is not defined here: `Column`'s `==` answers Filter, not Bool, so there is no inequality to derive. Declare `!=` beside it
   |
13 |   IO.printLine(email != "ada@example.com")
   |                ^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Give `Filter` a case for "not equal", and declare `!=` next to `==`:

```kex
type Filter = Equals(String, String) | NotEquals(String, String)

record Column do
  name : String
end

make Column do
  let ==(value: String) -> Filter = Equals(@name, value)
  let !=(value: String) -> Filter = NotEquals(@name, value)
end

main do
  let email = Column { name: "email" }
  IO.printLine(email != "ada@example.com")
end
```

This prints `NotEquals(email, ada@example.com)`.
