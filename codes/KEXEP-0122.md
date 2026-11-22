---
title: KEXEP-0122
---

The map that starts after `ages =` is missing its `}`. The parser only
notices on the next line, at `IO`, so the caret points there and not at
the end of the map.

```kex
main do
  let ages = { "ada": 36, "alan": 41
  IO.printLine(ages)
end
```

```
example.kex:3:3: [KEXEP-0122]: Error, expected '}' to close map, got UpperIdent [IO]
  |
3 |   IO.printLine(ages)
  |   ^^
```

A call left without its `)` is [KEXEP-0066](../KEXEP-0066/), the same
mistake with another bracket.

## Fixing it

```kex
main do
  let ages = { "ada": 36, "alan": 41 }
  IO.printLine(ages)
end
```
