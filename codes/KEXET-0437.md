---
title: KEXET-0437
---

`within:` sets how long a call to a server waits for its reply, in
milliseconds. `2.5` reads like two and a half seconds, but it is a `Float`,
and `within:` takes a whole number of milliseconds.

```kex
record ShoppingList do
  items : [String] = []
end

serving ShoppingList do
  slot items -> Reply<[String]> = { reply: @items }
end

foul show(list: Server<ShoppingList>) do
  IO.printLine(list.items(within: 2.5).to(String))
end
```

```
example.kex:10:35: [KEXET-0437]: Error, `within:` expects Integer milliseconds or :infinity, got Float
   |
10 |   IO.printLine(list.items(within: 2.5).to(String))
   |                                   ^^^
```

## Fixing it

Write the wait in milliseconds:

```kex
record ShoppingList do
  items : [String] = []
end

serving ShoppingList do
  slot items -> Reply<[String]> = { reply: @items }
end

foul show(list: Server<ShoppingList>) do
  IO.printLine(list.items(within: 2500).to(String))
end
```

If every call on `list` should wait that long, `list.within(2500)` gives a
handle that does, and its calls need no `within:` of their own.
