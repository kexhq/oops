---
title: KEXET-0462
---

`X` stands for any type, so `shout` has to work for every type it could
be given. `upperCase` exists only for some of them, such as `String`.

```kex
let shout(text: X) -> String = "${text.upperCase}!"
```

```
example.kex:1:40: [KEXET-0462]: Error, `upperCase` is not defined for every `X`, which stands for any type
  |
1 | let shout(text: X) -> String = "${text.upperCase}!"
  |                                   ^^^^^^^^^^^^^^
```

## Fixing it

If `shout` only makes sense for text, say so in its type:

```kex
let shout(text: String) -> String = "${text.upperCase}!"

main do
  IO.printLine(shout("hi"))
end
```
