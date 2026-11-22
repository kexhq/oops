---
title: KEXET-0180
---

`UserId` is a distinct type over `Integer`. `.as(UserId)` wraps an
`Integer` as a `UserId`, and nothing else. `"42"` is a `String`, and
`.as` does not parse text.

```kex
distinct type UserId = Integer

main do
  let id = "42".as(UserId)
  IO.printLine(id)
end
```

```
example.kex:4:19: [KEXET-0180]: Error, cannot convert String to UserId with `.as`
  |
4 |   let id = "42".as(UserId)
  |            ^^^^^^^^^^^^^^^
```

## Fixing it

Parse the text into an `Integer` first. Parsing can fail, so say what
happens then, and wrap the number:

```kex
distinct type UserId = Integer

main do
  let id = Integer.parse("42").or(0).as(UserId)
  IO.printLine(id)
end
```
