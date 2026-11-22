---
title: KEXET-0487
---

`clear` returns `Void`, so it is a cast: the message is sent and
`list.clear()` returns at once. Nothing waits for an answer, so there is no
wait for `within:` to limit.

```kex
record ShoppingList do
  items : [String] = []
end

serving ShoppingList do
  slot clear -> Void = New { items: [] }
end

foul reset(list: Server<ShoppingList>) = list.clear(within: 1000)
```

```
example.kex:9:61: [KEXET-0487]: Error, `within:` is not valid on an asynchronous cast slot
  |
9 | foul reset(list: Server<ShoppingList>) = list.clear(within: 1000)
  |                                                             ^^^^
```

## Fixing it

Drop `within:`:

```kex
record ShoppingList do
  items : [String] = []
end

serving ShoppingList do
  slot clear -> Void = New { items: [] }
end

foul reset(list: Server<ShoppingList>) = list.clear()
```

If the caller needs to know the list was cleared, make `clear` a call
instead, with a `Reply<...>` result. A call can take `within:`.
