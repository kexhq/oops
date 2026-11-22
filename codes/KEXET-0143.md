---
title: KEXET-0143
---

`.try` stops the function early when `Integer.parse` fails, and passes the
failure back to the caller. `double` returns a plain `Integer`, so there is
no way for it to say that it failed.

```kex
let double(text: String) -> Integer do
  let n = Integer.parse(text).try
  n * 2
end

main do
  IO.printLine(double("4"))
end
```

```
example.kex:2:34: [KEXET-0143]: Error, `.try` can fail, and `double` returns Integer, which cannot hold the failure: return a Result or an Optional, or handle it with `trying` or a `rescue`
  |
2 |   let n = Integer.parse(text).try
  |           ^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Let the function return an optional, and decide at the call what a failure
means:

```kex
let double(text: String) -> Integer? do
  let n = Integer.parse(text).try
  n * 2
end

main do
  IO.printLine(double("4").or(0))
end
```

If `double` should always return a number, drop `.try` and give a fallback
in place: `Integer.parse(text).or(0)`.
