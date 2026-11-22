---
title: KEXET-0420
---

A minus sign in front of a value negates a number. `heading` is a
`Direction`, and there is no negative `North`.

```kex
type Direction = North | South

main do
  let heading = North
  IO.printLine(-heading)
end
```

```
example.kex:5:16: [KEXET-0420]: Error, unary '-' requires a number, got Direction
  |
5 |   IO.printLine(-heading)
  |                ^^^^^^^^
```

## Fixing it

Here the minus was meant as "the other way". Write that as a function:

```kex
type Direction = North | South

let opposite(direction: Direction) -> Direction = match direction do
  North => South
  South => North
end

main do
  let heading = North
  IO.printLine(opposite(heading))
end
```

When the value holds a number, negate the number, as in `-price.cents`.
