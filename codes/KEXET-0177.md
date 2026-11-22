---
title: KEXET-0177
---

`Process.spawn` starts a server with the state it is given. `Inbox` on its own
is the name of the record type, not an inbox, so the server would have no
state to start from.

```kex
record Inbox do
  messages : [String] = []
end

serving Inbox do
  slot post(message: String) -> Void = New { messages: [message | @messages] }
end

main do
  let inbox = Process.spawn(Inbox)
  inbox.post("hello")
end
```

```
example.kex:10:29: [KEXET-0177]: Error, `Process.spawn(Inbox)` passes the type, not a value; spawn a server with its initial state: `Process.spawn(Inbox {})`
   |
10 |   let inbox = Process.spawn(Inbox)
   |                             ^^^^^
example.kex:11:3: [KEXET-0491]: Error, `post` expects argument 1 to be Inbox, but got Server<Type<Inbox>>

post : Inbox -> String -> Void

post : Server<Inbox> -> String -> Void
   |
11 |   inbox.post("hello")
   |   ^^^^^ this has type Server<Type<Inbox>>
```

The second error comes from the first. `inbox` is not a `Server<Inbox>`, so
`post` cannot be called on it. It goes away with the fix below.

## Fixing it

Pass an `Inbox` value. `Inbox {}` builds one with the field defaults:

```kex
record Inbox do
  messages : [String] = []
end

serving Inbox do
  slot post(message: String) -> Void = New { messages: [message | @messages] }
end

main do
  let inbox = Process.spawn(Inbox {})
  inbox.post("hello")
end
```
