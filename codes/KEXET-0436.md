---
title: KEXET-0436
---

`Integer.parse` gives a `Result`, and `.or` takes the value to use when it
is an `Error`. `defaultPort` is a function. `.or` does not call it, so
`port` would be the function and not a number.

```kex
let defaultPort(error: ParseError) -> Integer = 8080

main do
  let port = Integer.parse("80x").or(defaultPort)
  IO.printLine(port)
end
```

```
example.kex:4:38: [KEXET-0436]: Error, `or` needs a fallback of type Integer, but got a function. `or` never calls it, so the function itself would be the answer; pass a plain default, or `match` on the result to compute one
  |
4 |   let port = Integer.parse("80x").or(defaultPort)
  |                                      ^^^^^^^^^^^
```

A block in the same place is [KEXET-0434](../KEXET-0434/), and on an
optional this is [KEXET-0435](../KEXET-0435/).

## Fixing it

If the fallback is always 8080, pass the number:

```kex
main do
  let port = Integer.parse("80x").or(8080)
  IO.printLine(port)
end
```

If `defaultPort` needs the error, `match` on the result and call it in the
`Error` arm:

```kex
let defaultPort(error: ParseError) -> Integer = 8080

main do
  let port = match Integer.parse("80x") do
    Ok(number) => number
    Error(error) => defaultPort(error)
  end
  IO.printLine(port)
end
```
