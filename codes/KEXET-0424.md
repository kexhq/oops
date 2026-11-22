---
title: KEXET-0424
---

`IO` has no `println`. The compiler suggests the closest name it does have,
`print`.

```kex
main do
  IO.println("hi")
end
```

```
example.kex:2:13: [KEXET-0424]: Error, `IO` has no function `println`, did you mean `print`?
  |
2 |   IO.println("hi")
  |   ^^^^^^^^^^^^^^^^
```

The closest spelling is not always the one you want. `IO.print` does not
end the line. The function that does is `IO.printLine`.

## Fixing it

```kex
main do
  IO.printLine("hi")
end
```
