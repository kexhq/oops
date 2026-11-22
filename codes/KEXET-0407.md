---
title: KEXET-0407
---

`with` swaps in a stand-in for a capability inside its block, which is how a
test sends mail without sending it. `Mailer` is a plain `module`, and only a
module declared with `capability` can be replaced.

```kex
module Mailer do
  foul send(to: String, body: String) -> Bool do
    IO.printLine("sending to ${to}")
    return true
  end
end

record FakeMailer do
  sent : Integer = 0
end

make FakeMailer, implement: Mailer do
  foul send(to: String, body: String) -> Bool = true
end

foul welcome(user: String) -> Bool = Mailer.send(user, "Welcome!")

main do
  with Mailer = FakeMailer {} do
    IO.printLine(welcome("ada@example.com").to(String))
  end
end
```

```
example.kex:12:1: [KEXET-0130]: Error, unknown trait: Mailer
   |
12 | make FakeMailer, implement: Mailer do
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
example.kex:19:3: [KEXET-0407]: Error, 'Mailer' is not a capability, so it cannot be replaced by 'with'. Declare it as `capability Mailer do ... end`
   |
19 |   with Mailer = FakeMailer {} do
   |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

Both errors have the same cause. `implement: Mailer` fails too, because a
plain module is not something a record can implement.

## Fixing it

Declare `Mailer` as a capability. Nothing else changes:

```kex
capability Mailer do
  foul send(to: String, body: String) -> Bool do
    IO.printLine("sending to ${to}")
    return true
  end
end
```

Code outside a `with` block still runs the real `send`.
