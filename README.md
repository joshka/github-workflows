# GitHub workflows

This repository contains a collection of [reusable GitHub workflows] for use in Rust projects.

- [rust-check](#rust-check)
- [rust-release-plz](#rust-release-plz)
- [rust-test](#rust-test)

[reusable GitHub workflows]: https://docs.github.com/en/actions/using-workflows/reusing-workflows

## Rust Check

Checks:

- formatting using rustfmt
- lints using clippy and [rs-clippy-check](https://github.com/marketplace/actions/rs-clippy-check)
- docs (using nightly)
- msrv

[rust-check.yml](.github/workflows/rust-check.yml)

Usage:

```yaml
jobs:
  check:
    permissions:
      checks: write
    uses: joshka/github-workflows/.github/workflows/rust-check.yml@main
    with:
      msrv: 1.76.0 # this is optional defaults to 1.56.0
```

## Rust Test

[rust-test.yml](.github/workflows/rust-test.yml)

Tests:

- ubuntu with stable and beta
- mac / windows with stable
- minimal versions
- upload coverage to codecov.io (requires CODECOV_TOKEN)

```yaml
jobs:
  test:
    uses: joshka/github-workflows/.github/workflows/rust-test.yml@main
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

## Rust  Release-plz

Publishes the crate using [Release-plz]. Requires some setup see ...

[Release-plz]: https://release-plz.ieni.dev

```yaml
jobs:
  release-plz:
    uses: joshka/github-workflows/.github/workflows/rust-release-plz.yml@main
    permissions:
      pull-requests: write
      contents: write
    secrets:
      CARGO_REGISTRY_TOKEN: ${{ secrets.CARGO_REGISTRY_TOKEN }}
```
