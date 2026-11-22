---
title: KEXEF-0004
---

`spawn` starts a process, and that is a side effect. A plain `let` function
cannot have side effects, so it cannot use `spawn`. The `IO.printLine`
inside the block is a second error of the same kind.

```kex
let startWorker -> Integer do
  spawn do
    IO.printLine("working")
  end
  1
end
```

```
example.kex:2:3: [KEXEF-0004]: Error, cannot use 'spawn' in pure context
  |
2 |   spawn do
  |   ^^^^^^^^
example.kex:3:17: [KEXEF-0001]: Error, cannot call foul function 'IO.printLine' from pure context
  |
3 |     IO.printLine("working")
  |     ^^^^^^^^^^^^^^^^^^^^^^^
```

## Fixing it

Mark the function as `foul`. That fixes both errors:

```kex
foul startWorker -> Integer do
  spawn do
    IO.printLine("working")
  end
  1
end

main do
  IO.printLine(startWorker)
end
```
