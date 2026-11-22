---
title: KEXET-0120
---

There are two `log` functions. The one for a `String` is pure, and the
one for an `Integer` is `foul`. All the overloads of a name have to agree,
so that a call to `log` is either pure or foul whichever one it picks.

```kex
let log(message: String) = message
foul log(code: Integer) = IO.printLine("code ${code}")

main do
  log(404)
end
```

```
example.kex:2:6: [KEXET-0120]: Error, overloads of `log` must all have the same purity
  |
2 | foul log(code: Integer) = IO.printLine("code ${code}")
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Here the `String` version was meant to print too, so make it `foul`:

```kex
foul log(message: String) = IO.printLine(message)
foul log(code: Integer) = IO.printLine("code ${code}")

main do
  log("starting")
  log(404)
end
```

If one of them really is pure, it does something different, and it
should have its own name.
