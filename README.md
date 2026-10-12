# go-ooxml landing

Hugo source for **<https://go-ooxml.github.io/>** — the landing page of the
[`go-ooxml`](https://github.com/go-ooxml) org.

Preview locally:

```sh
hugo server
```

Build:

```sh
hugo --minify
```

The rendered site lives under `public/`, which is gitignored: GitHub Pages
builds it from this source (see `.github/workflows/deploy-pages.yml`).

## The design is not here

It comes from the shared Hugo module
[`go-fleettools/landingkit`](https://github.com/go-fleettools/landingkit),
pinned in `go.mod`. A landing that imports the module cannot drift from the
reference; it can only fall behind a version, and Renovate proposes the bump.

⛔ **`kit.go` is not optional.** A Hugo site has no Go code, so `go mod tidy`
finds nothing using the module and deletes the requirement — and the fleet's
Renovate presets run `gomodTidy` after every bump. The file exists only to be
seen by tidy; its build tag keeps it out of every build.

## The colours are read, not chosen

`landingkit brand static/img/logo.svg` derives `[params.brand]` from the
logo's own gradient. `go-ooxml` is in the **document family** — `go-odf`,
`go-richdoc`, `go-rtf`, `go-docutils` — and takes its `#4F46E5 → #1E1B4B`.
Backgrounds, surfaces, greys and borders belong to the shared sheet and cannot
be set here, which is deliberate: two landings once grew `surfaces` parameters
that tinted their backgrounds away from the reference.

Verified against `go-fileshare.github.io`, the reference:

```text
PASS the <style> block equals the reference's once brand values are masked
PASS light: 64/64 background pixels identical (#ffffff)
PASS dark: 64/64 background pixels identical (#0b0e14)
```
