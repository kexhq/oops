---
title: KEXET-0142
---

`.try` hands a failure back to the caller, so the function has to say what
it returns, and in a form that can hold a failure. `parse` has no return
type at all.

```kex
let parse(text: String) do
  let n = Integer.parse(text).try
  return n
end
```

```
example.kex:2:34: [KEXET-0142]: Error, `.try` can fail, and `parse` declares no result and `return`s: declare it, as `Integer?` or `Integer or! E`, or handle the failure with `trying` or a `rescue`
  |
2 |   let n = Integer.parse(text).try
  |           ^^^^^^^^^^^^^^^^^^^^^^^
```

A function that does declare a type, but one that cannot hold the failure,
gets [KEXET-0143](../KEXET-0143/).

## Fixing it

Declare the return type as an optional:

```kex
let parse(text: String) -> Integer? do
  let n = Integer.parse(text).try
  n
end

main do
  IO.printLine(parse("4").or(0))
end
```

Use `-> Integer or! E` instead when the caller should learn why it failed.
