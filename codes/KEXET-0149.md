---
title: KEXET-0149
---

`secret` is in the `private` block of `Config`, so only code inside
`Config` can use it. `limit`, which is public, can.

```kex
module Config do
  let limit = secret * 2

  private do
    let secret = 5
  end
end

main do
  IO.printLine(secret)
end
```

```
example.kex:10:16: [KEXET-0149]: Error, undefined name: `secret`. `Config.secret` is private to `Config`
   |
10 |   IO.printLine(secret)
   |                ^^^^^^
```

For a private function, the error is [KEXET-0166](../KEXET-0166/).

## Fixing it

Use a public name instead:

```kex
module Config do
  let limit = secret * 2

  private do
    let secret = 5
  end
end

main do
  IO.printLine(Config.limit)
end
```

If other code really needs `secret`, move it out of the `private` block.
