---
title: KEXET-0112
---

`Traffic.Light` has the constructors `Red`, `Amber` and `Green`. The
pattern `Traffic.Yellow` names one the module does not have.

```kex
module Traffic do
  type Light = Red | Amber | Green
end

let wait?(light: Traffic.Light) -> Bool do
  match light do
    Traffic.Red => true
    Traffic.Yellow => true
    _ => false
  end
end

main do
  IO.printLine(wait?(Traffic.Red))
end
```

```
example.kex:8:5: [KEXET-0112]: Error, `Traffic` has no constructor `Yellow`
  |
8 |     Traffic.Yellow => true
  |     ^^^^^^^^^^^^^^
```

## Fixing it

```kex
module Traffic do
  type Light = Red | Amber | Green
end

let wait?(light: Traffic.Light) -> Bool do
  match light do
    Traffic.Red => true
    Traffic.Amber => true
    _ => false
  end
end

main do
  IO.printLine(wait?(Traffic.Red))
end
```
