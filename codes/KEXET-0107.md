---
title: KEXET-0107
---

A `match` on a sum type leaves out one of its constructors. Kex rejects it
when the program is checked, rather than failing with no matching clause the
first time the missing case turns up at run time.

```kex
type Shade = Light | Tint(Integer)

let describe(shade: Shade) -> String do
  match shade do
    Tint(n) => "tint ${n}"
  end
end
```

```
example.kex:4:3: [KEXET-0107]: Error, non-exhaustive match on Shade: missing case(s) Light
  |
4 |   match shade do
  |   ^^^^^^^^^^^^^^
```

## Fixing it

Add an arm for each constructor the message lists:

```kex
let describe(shade: Shade) -> String do
  match shade do
    Light => "light"
    Tint(n) => "tint ${n}"
  end
end
```

Or, when the remaining cases really are all handled alike, end with `_`.
That arm also takes any constructor added to the type later, so prefer
naming the cases where that would hide a mistake.
