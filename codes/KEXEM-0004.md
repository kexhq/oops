---
title: KEXEM-0004
---

`withTax` is private to `Prices`. `Shop` can pass on the public `total`,
but it cannot make `withTax` public by listing it in `only:`.

```kex
module Prices do
  let total(net: Integer) -> Integer = withTax(net)

  private do
    let withTax(n: Integer) -> Integer = n + n / 5
  end
end

module Shop do
  export Prices, only: [total, withTax]
end

main do
  IO.printLine(Shop.Prices.total(100))
end
```

```
example.kex:10:3: [KEXEM-0004]: Error, cannot export private name `withTax` from Prices
   |
10 |   export Prices, only: [total, withTax]
   |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Export only `total`. It still calls `withTax` inside `Prices`:

```kex
module Prices do
  let total(net: Integer) -> Integer = withTax(net)

  private do
    let withTax(n: Integer) -> Integer = n + n / 5
  end
end

module Shop do
  export Prices, only: [total]
end

main do
  IO.printLine(Shop.Prices.total(100))
end
```

If other code needs `withTax` too, move it out of the `private` block.
