---
title: KEXET-0141
---

When a `.try` fails, the function returns early with the failure. `firstPort`
does not say what it returns, so Kex works it out, and here it cannot.
`lines.first.try` fails with `None`, an Optional's failure.
`Integer.parse(line).try` fails with an `Error`, a Result's failure. One
return type cannot be both.

```kex
let firstPort(lines: [String]) do
  let line = lines.first.try
  Integer.parse(line).try
end
```

```
example.kex:2:29: [KEXET-0141]: Error, `.try` can fail, and `firstPort` declares no result and mixes an Optional's `.try` with a Result's: declare it, as `Integer?` or `Integer or! E`, or handle the failure with `trying` or a `rescue`
  |
2 |   let line = lines.first.try
  |              ^^^^^^^^^^^^^^^
```

## Fixing it

Declare the result as `Integer?`, and turn the parse's Result into an
Optional with `.ok`, so both `.try`s fail the same way:

```kex
let firstPort(lines: [String]) -> Integer? do
  let line = lines.first.try
  Integer.parse(line).ok.try
end
```

A function with no declared result that uses `return` and `.try` together is
[KEXET-0142](../KEXET-0142/).
