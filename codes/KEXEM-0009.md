---
title: KEXEM-0009
---

`using Inventory` looks for a file that declares `module Inventory`, by its
name, `inventory.kex`, beside the file that uses it. There is no such file.

```kex
using Inventory

main do
  IO.printLine(Inventory.count)
end
```

```
example.kex:1:1: [KEXEM-0009]: Error, module not found in source roots: Inventory
  |
1 | using Inventory
  | ^^^^^^^^^^^^^^^
```

## Fixing it

Create `inventory.kex` next to the program, starting with the module line:

```kex
module Inventory

let count -> Integer = 3
```

Check the spelling if the file is there: `using Inventory` looks for
`inventory.kex`, and the file has to start with `module Inventory`.
