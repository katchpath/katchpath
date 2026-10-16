# katchpath

Stop `git add -A` from leaking your `.env`.

KatchPath is a tiny git guard. It refuses blanket adds from the wrong folder and blocks `.env` files, private keys, key-shaped strings (AWS, GitHub, GitLab, Stripe, OpenAI, Anthropic, Slack, Google, npm, SendGrid) and `node_modules` before they're staged or committed.

Free, MIT, one POSIX shell file, no dependencies.

## Install

```sh
curl -fsSL https://katchpath.com/install.sh | sh
# or
npm install -g katchpath
```

Then, in a repo:

```sh
katchpath install                              # pre-commit hook for this repo
katchpath install --global                     # or every repo (core.hooksPath)
echo 'eval "$(katchpath shell)"' >> ~/.zshrc   # guards git add -A / . / --all
```

Using the [pre-commit](https://pre-commit.com) framework? Add to `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/katchpath/katchpath
    rev: v0.1.5
    hooks:
      - id: katchpath
```

## Commands

```
katchpath install            install the pre-commit hook in this repo
katchpath install --global   install for every repo (git core.hooksPath)
katchpath shell              print the shell function that guards `git add -A/./--all`
katchpath scan [paths...]    check staged files (or the given paths)
katchpath add-check <args>   dry-run a `git add` and check what it would stage
katchpath version
```

Config: optional `.katchpath` at the repo root (`max_files`, `max_size_kb`, `scan_content`, `allow_roots`, `mode=block|warn`). Ignore list: `.katchpathignore`, one glob per line. Bypass once: `KATCHPATH_SKIP=1 git commit ...`.

## Free tools (in your browser)

- [API key scanner](https://katchpath.com/tools/api-key-scanner?src=gh): paste code or a diff, find leaked keys. Nothing is sent.
- [.env / .git exposure check](https://katchpath.com/tools/env-exposure-check?src=gh): is your live site serving `/.env` or `/.git/config`?
- [.gitignore tester](https://katchpath.com/tools/gitignore-tester?src=gh): which paths git ignores, and which rule decides.

## Already leaked something?

- [Committed a .env file to GitHub](https://katchpath.com/fix/committed-env-file-to-github?src=gh): rotate first, then clean history.
- [GitHub push protection: secret detected](https://katchpath.com/fix/github-push-protection-secret-detected?src=gh)
- [Prevent committing .env files](https://katchpath.com/fix/prevent-committing-env-file?src=gh)
- [Undo git add](https://katchpath.com/fix/undo-git-add?src=gh) · [Remove node_modules from git](https://katchpath.com/fix/remove-node-modules-from-git?src=gh) · [.gitignore not working](https://katchpath.com/fix/gitignore-not-working?src=gh)

## Teams

The [Team Pack](https://katchpath.com/buy?from=readme&src=gh) adds a GitHub Action that fails any PR adding a `.env` or key, a policy file and rollout scripts. $19, one-time.

## Licence

MIT
