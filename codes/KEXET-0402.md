---
title: KEXET-0402
---

`post` returns `Void`, which makes it a cast. A cast is sent without waiting,
so there is no caller to reply to, and `from` does not exist inside it.

```kex
record Inbox do
  messages : [String] = []
end

serving Inbox do
  foul slot post(message: String) -> Void do
    new.messages = [message | @messages]
    from.reply(new.messages.count)
    return new
  end
end
```

```
example.kex:8:5: [KEXET-0402]: Error, `from` is not available in a cast: no caller is waiting for a reply
  |
8 |     from.reply(new.messages.count)
  |     ^^^^
```

## Fixing it

If `post` should answer with the new count, make it a call. It returns
`Reply<Integer>`, and the reply goes in the result:

```kex
record Inbox do
  messages : [String] = []
end

serving Inbox do
  slot post(message: String) -> Reply<Integer> do
    new.messages = [message | @messages]
    return { new, reply: new.messages.count }
  end
end
```

If no one needs the count, keep the cast and delete the `from.reply` line.
