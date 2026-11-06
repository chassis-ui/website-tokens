# Changelog

The notable changes of each release of `@chassis-ui/website-tokens`, in the form of
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Written by hand, in the commit that
sets the version. The body of the GitHub release is the entry of its version, and a version
without an entry is not released.

The history of the token values before 0.1.0 is in the
[changelog of Chassis Tokens](https://github.com/chassis-ui/tokens/blob/main/packages/tokens/CHANGELOG.md).

## [0.4.0-next.0]

### Changed

- The `alternate` color context, a dark band in both modes, is tinted with the primary color:
  its backgrounds, text, borders, icons and cues come from the primary scale in place of the
  neutral scale, white and black. Its `base-color` is primary 80, with white on it, and
  `bg-disabled` follows `bg-evident`. Only values change, no token name.
- A push to `next` releases a version with a prerelease part, such as this one, to the npm
  dist-tag `next` and as a GitHub prerelease. `main` releases any other new version, as before.
- Built with `@chassis-ui/tokens` 0.16.0.

### Added

- `tools/`, two pages for making and checking color scales, in the repository and not in the
  package.

## [0.3.0]

### Changed

- **Breaking.** The Android libraries are named after the repository, as the zips:
  `chassis-tokens-demo-<brand>-<version>.aar` becomes
  `website-tokens-android-demo-<brand>-<version>.aar`. The zips, the Swift package and the package
  on npm keep their names, and no token changes.
- A release takes its text from this changelog, and stops without an entry.
- Built with `@chassis-ui/tokens` 0.15.0.

### Added

- `AGENTS.md`, with the rules for AI coding agents in this repository.

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
