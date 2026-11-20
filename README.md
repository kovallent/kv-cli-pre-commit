# kv-cli-pre-commit

[pre-commit](https://pre-commit.com) hooks for [kv-cli](https://github.com/kovallent/kv-cli), installed from its prebuilt binary wheels.

```yaml
repos:
  - repo: https://github.com/kovallent/kv-cli-pre-commit
    rev: v0.14.0
    hooks:
      - id: kv-cli            # audits staged Python, notebooks and config files
      - id: kv-cli-contract   # validates .kovallent.yaml when it changes
      - id: kv-cli-strict     # manual stage: pre-commit run kv-cli-strict --hook-stage manual --all-files
```

kv-cli's own hooks are `language: rust`, so pre-commit builds kv-cli from source on first run: every contributor needs Rust and a C compiler, and waits through a compile. This repository declares the same hooks, with the same `files` patterns, as `language: python` and pins `kv-cli==0.14.0`, which pip installs from the prebuilt wheels kv-cli publishes to PyPI (Linux x86_64 and aarch64, glibc and musl; macOS x86_64 and arm64; Windows x86_64). Nobody needs a toolchain and nothing compiles. A platform without a wheel falls back to building kv-cli's source distribution, which needs Rust again. This repository's version follows kv-cli's: tag `vX.Y.Z` pins `kv-cli==X.Y.Z`, and CI fails if the two ever differ.
