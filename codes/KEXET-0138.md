---
title: KEXET-0138
---

`Append` is one of the modes in `FS.FileMode`, and it lives in the `FS`
module. Outside `FS`, its constructors need the module name in front.

```kex
main do
  let file = FS.File.open("notes.txt", Append)
  IO.printLine(file.ok?)
end
```

```
example.kex:2:40: [KEXET-0138]: Error, `Append` is a constructor of FS.FileMode, declared in module FS: write `FS.Append`, or bring it in with `using FS`
  |
2 |   let file = FS.File.open("notes.txt", Append)
  |                                        ^^^^^^
```

## Fixing it

Write it with the module:

```kex
main do
  let file = FS.File.open("notes.txt", FS.Append)
  IO.printLine(file.ok?)
end
```

Or put `using FS` at the top of the file, and keep writing `Append`.
