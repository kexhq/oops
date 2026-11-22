---
title: KEXEL-0016
---

In a string, a backslash starts an escape such as `\n` or `\t`. The path
`C:\Users\ada` has a backslash before `U`, and `\U` is not an escape.

```kex
main do
  IO.printLine("C:\Users\ada")
end
```

```
example.kex:2:16: [KEXEL-0016]: Error, unknown escape '\U'; write '\\' for a backslash
  |
2 |   IO.printLine("C:\Users\ada")
  |                ^^^^^
```

Only the first bad escape is reported. `\a` would be next.

## Fixing it

Write each backslash twice:

```kex
main do
  IO.printLine("C:\\Users\\ada")
end
```

This prints `C:\Users\ada`.
