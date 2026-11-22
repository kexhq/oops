---
title: KEXET-0125
---

`latest` returns `Reply<String?>`, so whoever calls it waits for an answer.
The slot returns `{ new }`, which keeps the state and sends no reply, and it
never uses `from` to reply later. The caller would wait until it timed out.

```kex
record Inbox do
  messages : [String] = []
end

serving Inbox do
  slot latest -> Reply<String?> do
    return { new }
  end
end
```

```
example.kex:6:3: [KEXET-0125]: Error, call slot returns without `reply:` but never uses `from` for a deferred reply
  |
6 |   slot latest -> Reply<String?> do
  |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Reply in the result:

```kex
record Inbox do
  messages : [String] = []
end

serving Inbox do
  slot latest -> Reply<String?> = { reply: @messages.first }
end
```

A slot that has to answer later can return `{ new }` as long as it hands
`from` to something that will call `from.reply(...)`. Such a slot is a
`foul slot`.
