---
title: KEXET-0101
---

A method was called on a value whose type has no method by that name. This
often happens with names from other languages. Kex's names differ from
Ruby's in many places.

```kex
main do
  IO.printLine("hello".upcase)
end
```

```
example.kex:2:30: [KEXET-0101]: Error, undefined method `upcase` for `String`
  |
2 |   IO.printLine("hello".upcase)
  |                ^^^^^^^^^^^^^^
```

The message names the type the compiler sees. If that type isn't what you
expected, the value is the problem, not the method name. For example,
`list.first` is a `String?` in a list of strings, not a `String`.

## Fixing it

Use the method the type has:

```kex
main do
  IO.printLine("hello".upperCase)
end
```

`kex -s String` lists every method a `String` has.
