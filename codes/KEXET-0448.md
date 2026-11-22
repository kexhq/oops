---
title: KEXET-0448
---

A `while` condition has to be a `Bool`, and `queue.count` is an
`Integer`. Kex does not treat `0` as false.

```kex
main do
  var queue = [1, 2, 3]
  while queue.count do
    queue = queue.drop(1)
  end
  IO.printLine(queue)
end
```

```
example.kex:3:3: [KEXET-0448]: Error, while condition must be Bool, got Integer
  |
3 |   while queue.count do
  |   ^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Ask the question as a `Bool`:

```kex
main do
  var queue = [1, 2, 3]
  while !queue.empty? do
    queue = queue.drop(1)
  end
  IO.printLine(queue)
end
```
