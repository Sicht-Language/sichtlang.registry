# Sicht package registry

This repository lists libraries that Sicht programs can install. The package index is `registry.toml`, and package files are stored under `packages/`.

## Search for a package

Search by package name or description with:

```sh
sicht search math
```

Sicht searches the name and description in `registry.toml`. Search ignores case and matches part of a word. Each package version has its own entry, so results can include multiple versions of the same package.

Sicht uses this registry by default and keeps a local copy for later searches. Set `SICHT_REGISTRY` to use another registry address or a folder on your computer.

Install the newest listed version:

```sh
sicht install mathx
```

Install a specific version by adding `@` and the version:

```sh
sicht install mathx@1.0.0
```

## Package layout

Each version has its own folder. Put its `sicht.toml` manifest there. Put the library source in a subfolder named after the package.

```text
registry.toml
packages/
  <package-name>/
    <version>/
      sicht.toml
      <package-name>/
        <package-name>.si
```

For a library with several source files, use `package.si` as the entry file and put the other source files beside it:

```text
packages/<package-name>/<version>/
  sicht.toml
  <package-name>/
    package.si
    another_file.si
```

Example manifest:

```toml
[package]
name = "mathx"
version = "1.0.0"

[dependencies]
```

The package name and version in the manifest must match its folder names. Add required packages under `[dependencies]`.

## Add a package

1. Fork this repository and create a branch.
2. Create `packages/<package-name>/<version>/` using a new version number. Keep published version folders unchanged.
3. Add `sicht.toml` with the package name, version, and any dependencies.
4. Add the library source under `packages/<package-name>/<version>/<package-name>/`. Use `<package-name>.si` for a single source file, or `package.si` and additional files for a library with several files.
5. Add an entry for the new version to `registry.toml`:

   ```toml
   [[package]]
   name = "mathx"
   version = "1.0.0"
   description = "Basic math functions for Sicht"
   ```

   Keep the description short and useful. Sicht uses the name and description when searching. Match the version in the package folder and manifest.
6. Open a pull request against this repository. Describe the package, its version, and any platform requirements.

Include the new version folder and its matching entry in `registry.toml` in the pull request.