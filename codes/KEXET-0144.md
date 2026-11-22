---
title: KEXET-0144
---

`parse` says it returns an `Integer`. If `Integer.parse(price)` fails, `.try`
has to return the failure from `parse`, and an `Integer` has no room for one.

```kex
let cents(prices: [String]) do
  let parse(price: String) -> Integer = Integer.parse(price).try * 100
  prices.map(parse)
end
```

```
example.kex:2:66: [KEXET-0144]: Error, `.try` can fail, and this block returns Integer, which cannot hold the failure: return a Result or an Optional, or handle it with `trying` or a `rescue`
  |
2 |   let parse(price: String) -> Integer = Integer.parse(price).try * 100
  |                                         ^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Let `parse` return a Result, so the failure has somewhere to go:

```kex
let cents(prices: [String]) do
  let parse(price: String) -> Integer or! ParseError = Integer.parse(price).try * 100
  prices.map(parse)
end
```

`cents(["3", "x"])` then gives `[Ok(300), Error(...)]`. If a bad price should
count as zero instead, drop the `.try` and give a fallback:

```kex
let cents(prices: [String]) do
  let parse(price: String) -> Integer = Integer.parse(price).or(0) * 100
  prices.map(parse)
end
```
