---
title: KEXET-0422
---

`Billing` holds one module, `Tax`. `Billing.Taxes` asks for a module inside
it that does not exist.

```kex
module Billing do
  module Tax do
    let rate() -> Float = 0.2
  end
end

main do
  IO.printLine(Billing.Taxes.rate())
end
```

```
example.kex:8:29: [KEXET-0422]: Error, `Billing` has no module `Taxes`
  |
8 |   IO.printLine(Billing.Taxes.rate())
  |                ^^^^^^^^^^^^^
```

If `Billing` itself does not exist, the error is
[KEXET-0421](../KEXET-0421/) instead.

## Fixing it

```kex
module Billing do
  module Tax do
    let rate() -> Float = 0.2
  end
end

main do
  IO.printLine(Billing.Tax.rate())
end
```
