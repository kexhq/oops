---
title: KEXEM-0011
---

Kex finds a module by its file's path. `lib/store/billing.kex` is where
`Store.Billing` lives, but the file says `module Billing`. A module called
`Billing` would be in `lib/billing.kex`, so `using Billing` cannot find it.

`lib/store/billing.kex`:

```kex
module Billing

let invoice(total: Integer) -> String = "Due: ${total}"
```

`example.kex`:

```kex
using Billing

main do
  IO.printLine(invoice(40))
end
```

```
lib/store/billing.kex:1:1: [KEXEM-0011]: Error, module `Billing` is declared in a file whose path names `Store.Billing`, so `Billing` is not found; name it `module Store.Billing`, or move it to lib/billing.kex
  |
1 | module Billing
  | ^
```

## Fixing it

Either move the file to `lib/billing.kex` and keep `using Billing`, or keep
the file where it is and use the name its path gives it. In the file:

```kex
module Store.Billing

let invoice(total: Integer) -> String = "Due: ${total}"
```

And in `example.kex`:

```kex
using Store.Billing

main do
  IO.printLine(invoice(40))
end
```

Asking for `Store.Billing` without changing the file gives
[KEXEM-0010](../KEXEM-0010/).
