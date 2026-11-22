---
title: KEXEP-0103
---

In a pattern, a name that starts with a capital letter is a constructor,
like `Just` or `None`. So `Count` cannot be a new variable.

```kex
main do
  var Count = 0
  Count = Count + 1
  IO.printLine(Count)
end
```

```
example.kex:2:7: [KEXEP-0103]: Error, cannot bind 'Count' with 'var': patterns only bind lowercase names
  |
2 |   var Count = 0
  |       ^^^^^
```

## Fixing it

Start the name with a lowercase letter:

```kex
main do
  var count = 0
  count = count + 1
  IO.printLine(count)
end
```
