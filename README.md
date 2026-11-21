# oops

The Kex error and warning registry, published at <https://oops.kex.run>.

Every diagnostic the Kex compiler reports carries a stable code, and names it:

```
main.kex:4:21: [KEXET-0001]: Error, type mismatch: expected Integer, got String
```

`https://oops.kex.run/KEXET-0001` is that code's page. The site is a Tey
application: it reads the registry from the compiler itself, with
`kex --explain all --json`, so it lists exactly the codes the compiler that
ships reports, and it adds what the compiler cannot say in one line, a
hand-written explanation per code under [`codes/`](codes).

## Building it

It needs a `kex` whose `--explain all --json` exists (kex's `main`) and the
`tey` that came with it.

```sh
tey install          # fetches the markdown package
tey site:build       # writes the site to site/
tey site:serve       # serves site/ on http://localhost:4323
```

To build from a compiler that is not on `PATH`, or from a registry saved
earlier:

```sh
tey run -- build --out site --kex ../kex/build/kex
kex --explain all --json > registry.json
tey run -- build --out site --registry registry.json
```

## Explaining a code

An explanation is a Markdown file named for its code, `codes/KEXET-0001.md`:
what makes the compiler report it, an example that does, and how to fix it.
Every code's page links to the file to write or edit. The message itself is
not repeated there: it comes from the compiler.

## Publishing

`.github/workflows/pages.yml` builds Kex from `main`, builds the site and
deploys it to GitHub Pages: on a push here, nightly, and on a `registry`
repository dispatch, which kexhq/kex can send when its registry changes. The
site's `CNAME` is `oops.kex.run`.
