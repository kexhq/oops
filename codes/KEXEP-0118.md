---
title: KEXEP-0118
---

`&` is only for calling a method on each element, as in `&.upperCase`. To
pass a function you defined, such as `double`, capture it with `~`.

```kex
let double(n: Integer) -> Integer = n * 2

main do
  IO.printLine([1, 2, 3].map(&double))
end
```

```
example.kex:4:31: [KEXEP-0118]: Error, `&double` is no longer valid: write `~double` to capture a named function ('&' is receiver shorthand only, as in `&.method`)
  |
4 |   IO.printLine([1, 2, 3].map(&double))
  |                               ^^^^^^
```

## Fixing it

```kex
let double(n: Integer) -> Integer = n * 2

main do
  IO.printLine([1, 2, 3].map(~double))
end
```

`~double` is the function itself. `&.double` also works here, because
`n.double` is the same call as `double(n)`.
