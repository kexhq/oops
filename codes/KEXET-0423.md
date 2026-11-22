---
title: KEXET-0423
---

`IO` exists, but it has no function called `beep`.

```kex
main do
  IO.beep
end
```

```
example.kex:2:10: [KEXET-0423]: Error, `IO` has no function `beep`
  |
2 |   IO.beep
  |   ^^^^^^^
```

If the module has a function with a similar name, you get
[KEXET-0424](../KEXET-0424/), which suggests it. A module that does not
exist at all is [KEXET-0421](../KEXET-0421/).

## Fixing it

`kex -s IO` lists what `IO` has. For a module of your own, check how the
function is spelled where it is defined.
