---
title: KEXET-0001
---

A binding's value has a different type from the one its annotation names.
The annotation is what the rest of the program relies on, so the compiler
stops at the value that breaks it.

```kex
main do
  let count: Integer = "ten"
  IO.printLine(count)
end
```

```
example.kex:2:24: [KEXET-0001]: Error, type mismatch: expected Integer, got String
  |
2 |   let count: Integer = "ten"
  |              -------   ^^^^^ this has type String
  |              |
  |              expected because of this annotation
```

The message names the annotation's type first and the value's second.

An argument of the wrong type is [KEXET-0491](../KEXET-0491/), and a body
that answers something other than its signature says is
[KEXET-0127](../KEXET-0127/).

## Fixing it

Convert the value to the annotated type, deciding what happens when it
cannot be:

```kex
main do
  let count: Integer = "10".to(Integer).or(0)
  IO.printLine(count)
end
```

When the annotation is the part that is wrong, change it instead, or leave
it out and let the type be inferred.
