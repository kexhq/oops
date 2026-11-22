---
title: KEXET-0415
---

`scores.first` is an `Integer?`, because the list could be empty. `>`
compares two `Integer`s, and it has no answer for a value that might not be
there.

```kex
main do
  let scores = [3, 7]
  IO.printLine(scores.first > 5)
end
```

```
example.kex:3:31: [KEXET-0415]: Error, `>` is not defined for Integer? and Integer
  |
3 |   IO.printLine(scores.first > 5)
  |                ^^^^^^^^^^^^^^^^
```

For a type of your own that lacks the operator, the error is
[KEXET-0416](../KEXET-0416/), which says where to declare it.

## Fixing it

Decide what an empty list means, and give that value with `.or`:

```kex
main do
  let scores = [3, 7]
  IO.printLine(scores.first.or(0) > 5)
end
```

If the empty case needs its own branch, take the value out with
`if let Just(score) = scores.first`.
