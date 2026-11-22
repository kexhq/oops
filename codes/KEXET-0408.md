---
title: KEXET-0408
---

`FakeMailer` is meant to stand in for `Mailer`, but nothing says it can.
The stand-in on the right of `with` has to implement the capability.

```kex
capability Mailer do
  foul send(to: String, body: String) -> Bool do
    IO.printLine("sending to ${to}")
    return true
  end
end

record FakeMailer do
  sent : Integer = 0
end

foul welcome(user: String) -> Bool = Mailer.send(user, "Welcome!")

main do
  with Mailer = FakeMailer {} do
    IO.printLine(welcome("ada@example.com").to(String))
  end
end
```

```
example.kex:15:3: [KEXET-0408]: Error, replacement for capability 'Mailer' does not implement it: FakeMailer
   |
15 |   with Mailer = FakeMailer {} do
   |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Add a `make` block that implements every function of `Mailer` for
`FakeMailer`:

```kex
capability Mailer do
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

A `make` block that leaves out one of the functions is
[KEXET-0131](../KEXET-0131/).
