---
title: KEXET-0179
---

`.as(Atom)` makes its atom when the program is compiled, so it needs the
text written right there in quotes. `color` is a variable, and its value
is only known when the program runs.

```kex
main do
  let color = "red"
  IO.printLine(color.as(Atom))
end
```

```
example.kex:3:24: [KEXET-0179]: Error, `.as(Atom)` needs a string literal; for text known only at run time use `Atom.from(text)`, or `text.to(Atom)` to find an existing atom
  |
3 |   IO.printLine(color.as(Atom))
  |                ^^^^^^^^^^^^^^
```

## Fixing it

When the text is fixed, write it in place:

```kex
main do
  IO.printLine("red".as(Atom))
end
```

When it really comes from a variable, use `Atom.from(color)`, which makes
the atom, or `color.to(Atom)`, which gives an `Atom?` that is empty unless
the atom already exists. On the BEAM, atoms are never freed, so making
them from outside input, such as user text, can fill the atom table.
`.to(Atom)` is the safer choice there.
