---
title: KEXES-0004
---

`shout` is defined for `String` in two `make` blocks. When `"hi".shout`
is called, neither one wins, so the compiler stops at the second. The note
under the message points at the first.

```kex
make String do
  let shout -> String = "${this.upperCase}!"
end

make String do
  let shout -> String = "${this.upperCase}!!"
end
```

```
example.kex:6:3: [KEXES-0004]: Error, `shout` is defined twice for receiver `String`. The declaration form gives neither definition priority, so the call is ambiguous
  |
6 |   let shout -> String = "${this.upperCase}!!"
  |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
example.kex:2:3: note: the other definition is here
  |
2 |   let shout -> String = "${this.upperCase}!"
  |   ------------------------------------------
```

Defining a method the standard library already has is
[KEXET-0128](../KEXET-0128/).

## Fixing it

Keep one of them:

```kex
make String do
  let shout -> String = "${this.upperCase}!"
end

main do
  IO.printLine("hi".shout)
end
```
