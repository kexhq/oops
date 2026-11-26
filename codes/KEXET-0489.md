---
title: KEXET-0489
---

`withTax` is in the `private` part of `make Order`, so only the other
functions of that block can call it. `main` is outside the `Shop` module
altogether.

```kex
module Shop do
  record Order do
    total : Integer
  end

  make Order do
    let receipt = "Total: ${withTax(@total)}"

    private do
      let withTax(amount: Integer) = amount * 120 / 100
    end
  end
end

main do
  let order = Shop.Order { total: 50 }
  IO.printLine(order.withTax(order.total))
end
```

```
example.kex:17:16: [KEXET-0489]: Error, `withTax` is private to `make Shop.Order` in `Shop`. It is only callable inside that block
   |
17 |   IO.printLine(order.withTax(order.total))
   |                ^^^^^
```

## Fixing it

Call a public function that uses it:

```kex
module Shop do
  record Order do
    total : Integer
  end

  make Order do
    let receipt = "Total: ${withTax(@total)}"

    private do
      let withTax(amount: Integer) = amount * 120 / 100
    end
  end
end

main do
  let order = Shop.Order { total: 50 }
  IO.printLine(order.receipt)
end
```

If `main` really needs `withTax`, move it out of `private do`.
