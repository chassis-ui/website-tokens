# AGENTS.md

Instructions for AI coding agents working in this repository. It holds the rules an agent
breaks without being told; the README explains the rest.

## Project

@chassis-ui/website-tokens holds design tokens in the Tokens Studio format, in `source/`, synced with Figma. They
are built with [`@chassis-ui/tokens`](https://www.npmjs.com/package/@chassis-ui/tokens) into
`dist/<platform>/<app>/<brand>/`. `chassis.build` in `package.json` lists the brands, the themes,
the screens and the apps.

## Commands

Once, with Node.js 22.12 or later: `pnpm install`.

| Command                    | What it does                                        |
| -------------------------- | --------------------------------------------------- |
| `pnpm build`               | Builds the tokens into `dist/`                      |
| `pnpm lint`                | Checks the token files in `source/`                 |
| `pnpm verify`              | Fails when `dist/` differs from a fresh build       |
| `pnpm diff`                | Reports the tokens added, removed and changed       |
| `pnpm swift-package`       | Writes `Package.swift` from `chassis.build`         |
| `pnpm swift-package:check` | Fails when `Package.swift` differs from it          |
| `pnpm archive`             | Writes one zip per platform, app and brand          |
| `pnpm release-notes`       | Prints the changelog entry of the version, or fails |

## Rules

- **Edit `source/`, never `dist/`.** `dist/` and `Package.swift` are committed, and are the output
  of `pnpm build` and `pnpm swift-package`. Commit them with the change to `source/`.
- **`source/` follows Figma.** A sync from Figma writes these files, so a change that belongs in
  the design is made there. `$themes.json` and `$metadata.json` are written by Tokens Studio.
- **Keep `chassis.build` in step with `$themes.json`.** A brand, an app, a theme or a screen is
  in both.
- **The names in `dist/` are public.** Apps read them by name, and a removed or renamed token
  stops them compiling. `pnpm diff` names such a change, and the changelog says so.

## Branches

- `main` holds the released versions, and takes a change by pull request only.
- `next` is the prerelease channel. Work is merged into it first, and it is merged into `main`
  with a merge commit, never a squash, so the two keep one history.
- Any other branch is short-lived, `feat/…`, `fix/…` or `chore/…`, and is squash-merged.
- A design draft branch, such as `figma-next`, is synced from another Figma file and is outside
  this flow. Never merge it, and never take its `source/$themes.json`, which refers to that file:
  only its brand files are carried over, by hand. Leave such a branch alone.

## Releases

A push to `main` or `next` with a new version in `package.json` releases it and publishes it to
npm, so:

- On `next`, only a version with a prerelease part, such as `0.4.0-next.0`, is released, as a
  prerelease; on `main`, any new version. Each version, a prerelease too, has its entry.
- A new version and its entry in `CHANGELOG.md` go in one commit. The release stops without the
  entry.
- Before that commit, run `pnpm build`, which writes the version into `dist/`, and
  `pnpm verify`.
- Do not push, tag or raise the version unless asked.
