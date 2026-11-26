# Contributing to Salvanza

Thank you for helping. This page says where changes go and what to check before you send them.

## Branches: pull requests go to `develop`

- **`develop`** is where all work happens. Base your branch on it and open your pull request against it.
- **`master`** only takes releases. Changes reach it when a version is released, so a pull request against `master` will be asked to move.
- GitHub may suggest `master` as the base when you open a pull request. If it does, choose `develop` instead (or, on a pull request already open, **Edit** next to its title and change the base).
- Before you open it, bring your branch up to date: `git fetch upstream`, then `git rebase upstream/develop`.

## Before you open a pull request

- **Tests pass.** `make test` runs the Go tests of every module. For changes to the app's screens, also run the tests in `gui/frontend` with `node src/<name>.test.mjs` (for example `node src/manuals.test.mjs`).
- **Go code is formatted** with `gofmt`; the CI checks every Go file.
- **No build output.** Leave out `gui/frontend/dist/`, `gui/frontend/wailsjs/` and `gui/build/bin/`: they are rebuilt from the sources.
- **One change per pull request**, with a description of what it does, why, and how you tested it. Link the issue it fixes (`Fixes #123`).
- **Behaviour changes are documented.** Update the manuals in `docs/manual/` and copy the changed file to `gui/docs/manual/` (the app embeds those copies; `TestEmbeddedManualsMatchDocs` fails while they differ). Add a line to `CHANGELOG.md`.

`AGENTS.md` describes the repository's layout, build and conventions in more detail.

## Translations

The app's texts are in `gui/frontend/src/i18n/translations.js`, one block per language. English is the source.

- **Every language needs every English text.** Keep placeholders such as `{pbs}` or `{count}` exactly as they are, and leave product names untranslated.
- **A new language** uses the first part of the system's language code as its key, because that is how the app picks the language automatically: `zh`, not `zhcn` or `zh-CN`. Add it to `gui/frontend/src/components/LanguageSwitcher.jsx` with its name written in that language (for example 简体中文), a flag in `gui/frontend/src/assets/flags/`, and update the language count in `gui/frontend/src/aboutBrand.test.mjs`.
- **Translated READMEs** are made from the English `README.md`; where they differ, the English one is current.

## Commit messages

One line saying where and what, in plain words, then a short explanation of why if it is not obvious. For example:

```
pbscommon: private mount check uses slash paths on every system
```

## Reporting a problem

Open an issue on GitHub with the version (**About** in the app, or `salvanza-cli version`), the system it runs on, what you did and what happened. Logs help; remove any passwords or tokens from them first.

## Licence

Salvanza is licensed under the GPLv3. By contributing, you agree that your contribution is licensed under the same terms.
