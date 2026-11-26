---
title: KEXET-0142
---

A function that declares no result can usually leave it to the compiler,
even with a `.try` in it: the failure becomes part of the result it
works out. `parse` also leaves early with `return`, and that exit gives a
plain `Integer`, not one wrapped to sit beside a failure. No one result
fits both exits, so `parse` has to say what it returns.

```kex
let parse(text: String) do
  return 0 if text.empty?
  Integer.parse(text).try
end
```

```
example.kex:3:26: [KEXET-0142]: Error, `.try` can fail, and `parse` declares no result and `return`s: declare it, as `Integer?` or `Integer or! E`, or handle the failure with `trying` or a `rescue`
  |
3 |   Integer.parse(text).try
  |   ^^^^^^^^^^^^^^^^^^^^^^^
```

A function that does declare a type, but one that cannot hold the failure,
gets [KEXET-0143](../KEXET-0143/).

## Fixing it

Declare the return type as an optional, and wrap the early value in `Just`
to fit it:

```kex
let parse(text: String) -> Integer? do
  return Just(0) if text.empty?
  Integer.parse(text).try
end

main do
  IO.printLine(parse("4").or(0))
end
```

Use `-> Integer or! E` instead when the caller should learn why it failed.
