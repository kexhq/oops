---
title: KEXEF-0001
---

A function that isn't marked `foul` calls one that is. A `foul` function has
side effects, such as printing, reading files or talking to the network. A
plain `let` function can't have any, so it can't call one.

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

Everything in `IO` is `foul`. `main` can call `foul` functions.

## Fixing it

Declare the function with `foul` instead of `let`:

```kex
foul greet(name: String) -> Void = IO.printLine("hello, ${name}")

main do
  greet("Ada")
end
```

Often a better fix is to keep the function pure and let the caller do the
printing. A function that builds the text, called as
`IO.printLine(greeting("Ada"))` in `main`, is easier to test.

For debugging, `IO.inspect` can be used anywhere, pure code included.
