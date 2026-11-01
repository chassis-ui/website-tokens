# Changelog

The notable changes of each release of `@chassis-ui/website-tokens`, in the form of
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Written by hand, in the commit that
sets the version.

The history of the token values before 0.1.0 is in the
[changelog of Chassis Tokens](https://github.com/chassis-ui/tokens/blob/main/packages/tokens/CHANGELOG.md).

## [0.2.0]

### Added

- One zip per platform, app and brand, attached to each release:
  `website-tokens-<platform>-<app>-<brand>-<version>.zip`, with the content of
  `dist/<platform>/<app>/<brand>/` at its top level. `pnpm archive` writes them to `archives/`.

### Changed

- A release runs on a push to `main` with a new version in `package.json`, in place of a tag
  pushed by hand. The workflow creates the tag `v<version>`, and a push whose version has a tag
  releases nothing.
- Built with `@chassis-ui/tokens` 0.14.0.

## [0.1.0]

### Added

- The tokens of the Chassis websites and apps, moved from `@chassis-ui/tokens`, with the values
  of its 0.11.0: the `source/` files and the `dist/` output of the `chassis` and `sinefil`
  brands, the `docs` app on the web and the `demo` app on iOS and Android.
- The Swift package of this repository, with `Package.swift` at its root and the libraries
  `ChassisTokensDemoChassis` and `ChassisTokensDemoSinefil`.
- The Android libraries, `chassis-tokens-demo-<brand>-<version>.aar`, attached to each release.
