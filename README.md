# Dotfiles (Simon Taggart)

My macOS dotfiles.

## How to install

The installation step requires the [XCode Command Line
Tools](https://developer.apple.com/downloads) and may overwrite existing
dotfiles in your HOME.

```bash
$ bash -c "$(curl -fsSL https://raw.githubusercontent.com/SiTaggart/dotfiles/main/bin/dotfiles)"
```

N.B. If you wish to fork this project and maintain your own dotfiles, you must
substitute my username for your own in the above command and the 2 variables
found at the top of the `bin/dotfiles` script.

## How to update

You should run the update when:

- You make a change to `~/.dotfiles/git/gitconfig` (the only file that is
  copied rather than symlinked).
- You want to pull changes from the remote repository.
- You want to update Homebrew formulae and global packages.

Run the dotfiles command:

```bash
$ dotfiles
```

Options:

<table>
    <tr>
        <td><code>-h</code>, <code>--help</code></td>
        <td>Help</td>
    </tr>
    <tr>
        <td><code>-l</code>, <code>--list</code></td>
        <td>List of additional applications to install</td>
    </tr>
    <tr>
        <td><code>--no-packages</code></td>
        <td>Suppress package updates</td>
    </tr>
    <tr>
        <td><code>--no-sync</code></td>
        <td>Suppress pulling from the remote repository</td>
    </tr>
</table>

## Features

## Inspiration / modernization notes

See `docs/inspiration.md` for a menu of common dotfiles patterns and settings you may want to adopt.

### Automatic software installation

Homebrew formulae:

- Managed by `lib/brew` (formulae + casks), including: coreutils, git, bash, node, fnm, gh, mas, postgresql, zsh, ripgrep.

Global packages:

- Managed by `lib/bun` (global packages installed with bun).

### Custom macOS defaults

Custom macOS settings can be applied during the `dotfiles` process. They can
also be applied independently by running the following command:

```bash
$ osxdefaults
```

### Bootable backup-drive script

These dotfiles include a script that uses `rsync` to incrementally back up your
data to an external, bootable clone of your computer's internal drive. First,
make sure that the value of `DST` in the `bin/backup` script matches the name
of your backup-drive. Then run the following command:

```bash
$ backup
```

For more information on how to setup your backup-drive, please read the
preparatory steps in this post on creating a [Mac OS X bootable backup
drive](http://nicolasgallagher.com/mac-osx-bootable-backup-drive-with-rsync/).

### iTerm Color Theme

Use Oceanic Next iTerm port, found here: [https://github.com/mhartington/oceanic-next-iterm](https://github.com/mhartington/oceanic-next-iterm)

### ZSH and oh-my-zsh custom prompt

The `.zshrc` is configured for oh-my-zsh with the Powerlevel10k theme.

### Local/private Bash

Any private and custom Bash commands and configuration should be placed in a
`~/.bash_profile.local` file. This file will not be under version control or
committed to a public repository. If `~/.bash_profile.local` exists, it will be
sourced for inclusion in `bash_profile`.

Here is an example `~/.bash_profile.local`:

```bash
# PATH exports
PATH=$PATH:~/.gem/ruby/1.8/bin
export PATH

# Git credentials
# Not under version control to prevent people from
# accidentally committing with your details
GIT_AUTHOR_NAME="Simon Taggart"
GIT_AUTHOR_EMAIL="simon@example.com"
GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
# Set the credentials (modifies ~/.gitconfig)
git config --global user.name "$GIT_AUTHOR_NAME"
git config --global user.email "$GIT_AUTHOR_EMAIL"

# Aliases
alias code="cd ~/Code"
```

N.B. Because the `git/gitconfig` file is copied to `~/.gitconfig`, any private
git configuration specified in `~/.bash_profile.local` will not be committed to
your dotfiles repository.

### Custom location for Homebrew installation

If your Homebrew installation is not in `/usr/local` then you must prepend your
custom installation's `bin` to the PATH in a file called `~/.dotfilesrc`:

```bash
# Add `brew` command's custom location to PATH
PATH="/opt/acme/bin:$PATH"
```

## Acknowledgements

Inspiration and code was taken from many sources, including:

- [@mathiasbynens](https://github.com/mathiasbynens) (Mathias Bynens)
  [https://github.com/mathiasbynens/dotfiles](https://github.com/mathiasbynens/dotfiles)
- [@tejr](https://github.com/tejr) (Tom Ryder)
  [https://github.com/tejr/dotfiles](https://github.com/tejr/dotfiles)
- [@gf3](https://github.com/gf3) (Gianni Chiappetta)
  [https://github.com/gf3/dotfiles](https://github.com/gf3/dotfiles)
- [@cowboy](https://github.com/cowboy) (Ben Alman)
  [https://github.com/cowboy/dotfiles](https://github.com/cowboy/dotfiles)
- [@alrra](https://github.com/alrra) (Cãtãlin Mariş)
  [https://github.com/alrra/dotfiles](https://github.com/alrra/dotfiles)
