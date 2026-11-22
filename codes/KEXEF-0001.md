---
title: KEXEF-0001
---

`greet` is a plain `let` function, so it cannot have side effects, and
printing is one. Everything in `IO` is `foul`, and only `foul` functions and
`main` can call them.

```kex
let greet(name: String) -> Void = IO.printLine("hello, ${name}")

main do
  greet("Ada")
end
```

```
example.kex:1:47: [KEXEF-0001]: Error, cannot call foul function 'IO.printLine' from pure context
  |
1 | let greet(name: String) -> Void = IO.printLine("hello, ${name}")
  |                                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Make `greet` a `foul` function:

```kex
foul greet(name: String) -> Void = IO.printLine("hello, ${name}")

main do
  greet("Ada")
end
```

You can also keep `greet` pure: have it return the text, and print that in
`main`. Pure functions are easier to test.

`IO.inspect` is the exception. It can be called from anywhere, for
debugging.
