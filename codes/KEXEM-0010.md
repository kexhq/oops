---
title: KEXEM-0010
---

`using Store.Billing` finds `lib/store/billing.kex`, as it should. But the
file inside declares `module Billing`, not `Store.Billing`, so it is not
the module that was asked for.

`lib/store/billing.kex`:

```kex
module Billing

let invoice(total: Integer) -> String = "Due: ${total}"
```

`example.kex`:

```kex
using Store.Billing

main do
  IO.printLine(invoice(40))
end
```

```
lib/store/billing.kex:1:1: [KEXEM-0010]: Error, this file is `Store.Billing` by its path, but declares `Billing`; name it `module Store.Billing`
  |
1 | module Billing
  | ^
```

## Fixing it

Give the module the full name its path gives it:

```kex
module Store.Billing

let invoice(total: Integer) -> String = "Due: ${total}"
```

Asking for `Billing` instead, with the file unchanged, gives
[KEXEM-0011](../KEXEM-0011/).
