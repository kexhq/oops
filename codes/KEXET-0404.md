---
title: KEXET-0404
---

`new` is a copy of `this` that exists only in a `make` block for a record.
`moved` is an ordinary function, so there is no `new` in it and no field to
assign.

```kex
record Point do
  x : Integer
  y : Integer
end

let moved(p: Point) -> Point do
  new.x = p.x + 1
  new
end
```

```
example.kex:7:3: [KEXET-0413]: Error, field assignment requires a record binding
  |
7 |   new.x = p.x + 1
  |   ^^^^^^^^^^^^^^^
example.kex:8:3: [KEXET-0404]: Error, `new` requires a record receiver (or an explicit local binding)
  |
8 |   new
  |   ^^^
```

The assignment fails first, with [KEXET-0413](../KEXET-0413/). The `new` on
the last line is this error.

## Fixing it

Make your own copy in a `var` and change that:

```kex
record Point do
  x : Integer
  y : Integer
end

let moved(p: Point) -> Point do
  var copy = p
  copy.x = p.x + 1
  copy
end

main do
  IO.printLine(moved(Point { x: 1, y: 2 }).x)
end
```

The copy may even be called `new`, as in `var new = p`. That is the
"explicit local binding" in the message. Or move `moved` into a `make Point`
block, where `new` is there for you:

```kex
record Point do
  x : Integer
  y : Integer
end

make Point do
  let moved -> Point do
    new.x = @x + 1
    new
  end
end

main do
  IO.printLine(Point { x: 1, y: 2 }.moved.x)
end
```
