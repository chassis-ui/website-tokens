# @chassis-ui/website-tokens

The design tokens of the Chassis websites and apps: the `chassis` and `sinefil` brands, the
`docs` app on the web and the `demo` app on iOS and Android. They are
[Tokens Studio](https://tokens.studio) files, synced with Figma and built with
[`@chassis-ui/tokens`](https://www.npmjs.com/package/@chassis-ui/tokens) into SCSS, Swift and
Android resources.

## Layout

```
source/$themes.json            The brand, app, theme and screen options, from Tokens Studio
source/$metadata.json          The order of the token sets, from Tokens Studio
source/<group>/<set>.json      The token sets, from Tokens Studio
dist/<platform>/<app>/<brand>/ The output of a build, committed and published
Package.swift                  The Swift package of the iOS output, written by a command
package.json                   The brands, apps, themes and screens, in `chassis.build`
```

A designer syncs `source/` from Figma with Tokens Studio. The options `default`, `demo-a` and
`demo-b` of the brand group are in the source and not in `chassis.build`, so they are not
built. Do not edit `dist/` or `Package.swift` by hand.

## Commands

Once, with Node.js 22.12 or later:

```shell
pnpm install
```

| Command                    | What it does                                                            |
| -------------------------- | ----------------------------------------------------------------------- |
| `pnpm build`               | Builds every brand, app and platform into `dist/`                       |
| `pnpm lint`                | Checks the token files in `source/`                                     |
| `pnpm verify`              | Checks that a fresh build equals the committed `dist/`                  |
| `pnpm diff`                | Reports the tokens added, removed and changed against the `main` branch |
| `pnpm swift-package`       | Writes `Package.swift` from `chassis.build`                             |
| `pnpm swift-package:check` | Checks that `Package.swift` follows `chassis.build`                     |
| `pnpm archive`             | Writes one zip per platform, app and brand of `dist/` to `archives/`    |

`node_modules/.bin/chassis-tokens build --help` prints the options of the build: a part of the
output with `--brand`, `--app`, `--platform`, `--theme` and `--screen`, and a plan with
`--dry-run`.

After a change to the tokens, run `pnpm build` and commit `source/` and `dist/` together.
`pnpm verify` ignores the timestamp and the version in the file headers, so a build that
changes nothing else needs no commit.

## Use

Web, with Sass modules, from `npm install @chassis-ui/website-tokens`:

```scss
@use '@chassis-ui/website-tokens/dist/web/docs/chassis/main' as tokens;

.card {
  padding: tokens.$cx-space-context-medium;
}
```

iOS: add `https://github.com/chassis-ui/website-tokens.git` with Swift Package Manager, then
the library `ChassisTokensDemoChassis` or `ChassisTokensDemoSinefil`. The version is the tag.

Android: download `chassis-tokens-demo-<brand>-<version>.aar` from the
[GitHub release](https://github.com/chassis-ui/website-tokens/releases).

A project that takes the files of one brand: download
`website-tokens-<platform>-<app>-<brand>-<version>.zip` from the same release.

The [documentation of Chassis Tokens](https://chassis-ui.com/tokens/) describes the tokens, the
output of each platform and how a project uses it.

## Releases

A release is a push to `main` with a new version in `package.json`, without a tag of its own, as
the workflow makes the tag:

1. Set the version in `package.json`, and add its entry to `CHANGELOG.md`.
2. `pnpm build`, which writes the version into the headers of `dist/`. `pnpm verify` ignores
   those lines, so it does not notice a build that was skipped.
3. `pnpm verify`.
4. Commit all of it, then `git push origin main`.

The release workflow runs when the version has no tag `v<version>`. It lints `source/`, checks
`dist/` against a fresh build and `Package.swift` against `chassis.build`, builds the Android
libraries with the Gradle project that comes with `@chassis-ui/tokens`, writes the archives,
publishes the package to npm with trusted publishing, and creates the tag and its GitHub release
with one Android library per app and brand, and one zip per platform, app and brand, attached.
A push whose version has a tag releases nothing, and a release that fails makes no tag, so the
next push tries again. A version with a prerelease part, such as `0.2.0-next.0`, goes to the
dist-tag `next`.

The trusted publisher of the package on npmjs.com is this repository and `release.yml`.
Renaming the workflow file breaks publishing until it is updated there.

## Changes

[CHANGELOG.md](CHANGELOG.md) lists each release from 0.1.0, written by hand in the commit that
sets the version. The history of the token values before 0.1.0 is in the
[changelog of Chassis Tokens](https://github.com/chassis-ui/tokens/blob/main/packages/tokens/CHANGELOG.md),
and the commits of `source/` and `dist/` came along with them in `git log`.

## License

MIT License — see the [LICENSE](LICENSE) file for details.
