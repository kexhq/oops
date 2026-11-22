---
title: KEXET-0157
---

The `Course` type is written after `end`, outside `module Menu`. `price`
can still use it, because it is in the same file. A program that says
`using Menu` cannot see `Course` or its constructor `Soup`.

`lib/menu.kex`:

```kex
module Menu do
  let price(course: Course) -> Integer do
    match course do
      Soup => 5
      Roast => 12
    end
  end
end

type Course = Soup | Roast
```

`example.kex`:

```kex
using Menu

main do
  IO.printLine(price(Soup))
end
```

```
example.kex:4:22: [KEXET-0157]: Error, undefined constructor or type: `Soup`. menu.kex declares it outside its module, for itself
  |
4 |   IO.printLine(price(Soup))
  |                      ^^^^
```

## Fixing it

Declare the type inside the module:

```kex
module Menu do
  type Course = Soup | Roast

  let price(course: Course) -> Integer do
    match course do
      Soup => 5
      Roast => 12
    end
  end
end
```

Functions declared outside the module give [KEXET-0168](../KEXET-0168/).
