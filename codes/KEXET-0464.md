---
title: KEXET-0464
---

`scores.first` is an `Integer?`, because the list could be empty, and `+`
does not reach inside an optional. Both sides of `+` must have the same
type. Numbers are the exception: an `Integer` and a `Float` add up to a
`Float`.

```kex
main do
  let scores = [3, 5, 8]
  IO.printLine(10 + scores.first)
end
```

```
example.kex:3:21: [KEXET-0464]: Error, operator '+' requires matching types, got Integer and Integer?
  |
3 |   IO.printLine(10 + scores.first)
  |                ^^^^^^^^^^^^^^^^^
```

Adding a `String` to something that is not text is
[KEXET-0463](../KEXET-0463/).

## Fixing it

Say what to add when the list is empty. `.or` gives a plain `Integer`:

```kex
main do
  let scores = [3, 5, 8]
  IO.printLine(10 + scores.first.or(0))
end
```
