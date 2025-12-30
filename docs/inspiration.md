# Dotfiles inspiration (menu of options)

This is a shortlist of common patterns and “high-signal” tweaks found in popular dotfiles repos, so you can pick what you want to add next.

**Repos sampled**

- `mathiasbynens/dotfiles` (notably `.macos`, `brew.sh`, `bootstrap.sh`)
- `holman/dotfiles` (notably `script/bootstrap`, `Brewfile`)
- `driesvints/dotfiles` (notably `.macos`, `.zshrc`, `Brewfile`)
- `paulirish/dotfiles` (notably `.macos`, `brew.sh`)
- `thoughtbot/dotfiles` (notably `gitconfig`, `zshrc`)

## Common repo patterns

### 1) Brewfile-first package management

Many repos converge on `Brewfile` + `brew bundle` as the “source of truth” for installed tools/apps.

Why it’s useful:

- Idempotent: re-run safely.
- Easier to review changes in PRs (diffable list vs imperative script logic).
- Handles formulae, casks, and Mac App Store apps (via `mas`).

Typical shape:

- `Brewfile` contains `tap`, `brew`, `cask`, `mas` entries.
- A bootstrap script runs `brew bundle` after Homebrew is installed.

### 2) Separate “bootstrap” vs “daily shell config”

Most repos separate:

- bootstrap/install steps (Homebrew, packages, macOS defaults) from
- interactive shell settings (aliases, functions, prompt).

This reduces “surprise side effects” every time a shell launches.

### 3) Local/private overrides that never get committed

Common patterns:

- `~/.zshrc.local` / `~/.bash_profile.local` for machine-specific and secret values.
- `~/.gitconfig.local` included from the tracked `.gitconfig`.

### 4) A macOS defaults script that’s deliberately curated

The `.macos`/`osxdefaults` script in many repos:

- focuses on a small number of high-confidence settings
- avoids disabling security protections by default
- expects some preferences to break on newer macOS

## Common CLI tools people install (via Brewfile)

Frequently seen “baseline” CLI set (choose what you like):

- Search/navigation: `ripgrep`, `fd`, `fzf`, `zoxide`
- Better defaults: `bat`, `eza`, `jq`
- Dev workflow: `gh`, `git`, `gpg`, `shellcheck`
- Env mgmt: `mise` or `asdf` (language version management), `direnv`
- Shell UX: `atuin` (history), `starship` (prompt) _or_ oh-my-zsh + powerlevel10k

## macOS defaults ideas (pick-and-choose)

These are examples of settings that show up repeatedly across other dotfiles repos. macOS 26 (“Tahoe”) may ignore some keys; treat these as “try and keep if they still work”.

### Finder

- Show POSIX path bar: `defaults write com.apple.finder ShowPathbar -bool true`
- Default search scope to current folder: `defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"`
- Warn before emptying the Trash: `defaults write com.apple.finder WarnOnEmptyTrash -bool true`
- Disable animations: `defaults write com.apple.finder DisableAllAnimations -bool true`

### Dock / Mission Control

- Auto-hide without delay: `defaults write com.apple.dock autohide-delay -float 0`
- Faster auto-hide animation: `defaults write com.apple.dock autohide-time-modifier -float 0.2`
- Minimize windows into application icon: `defaults write com.apple.dock minimize-to-application -bool true`
- Reduce resize animation time: `defaults write NSGlobalDomain NSWindowResizeTime -float 0.001`

### Save/print panels

- Expand Save panel by default: `defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true`
- Expand Save panel by default (newer key): `defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode2 -bool true`
- Expand Print panel by default: `defaults write NSGlobalDomain PMPrintingExpandedStateForPrint -bool true`
- Expand Print panel by default (newer key): `defaults write NSGlobalDomain PMPrintingExpandedStateForPrint2 -bool true`

### Screenshots

- Disable shadow: `defaults write com.apple.screencapture disable-shadow -bool true`

### Security note (common but not recommended)

- Disabling quarantine prompts is common in older dotfiles, but it weakens macOS protections:
  - `defaults write com.apple.LaunchServices LSQuarantine -bool false`
  - Recommended: leave this alone unless you’re sure you want it.

## Suggested next upgrades for this repo (low-risk, high-value)

If you want “modernization with the least churn”, these usually pay off quickly:

- Add a `Brewfile` and switch `lib/brew` to `brew bundle` (keep your current list, but in declarative form).
- Add `fzf` + `zoxide` + `bat` + `fd` + `shellcheck` to your base toolset.
- Add an explicit `~/.gitconfig.local` include so identity/signing can be per-machine.
- Add a “dry-run / audit” mode for `bin/dotfiles` (prints what it would do without changing anything).
