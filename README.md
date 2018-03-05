# Dotfiles (Simon Taggart)

My OS X dotfiles.


## How to install

The installation step requires the [XCode Command Line
Tools](https://developer.apple.com/downloads) and may overwrite existing
dotfiles in your HOME.

```bash
$ bash -c "$(curl -fsSL raw.github.com/SiTaggart/dotfiles/master/bin/dotfiles)"
```

N.B. If you wish to fork this project and maintain your own dotfiles, you must
substitute my username for your own in the above command and the 2 variables
found at the top of the `bin/dotfiles` script.

## How to update

You should run the update when:

* You make a change to `~/.dotfiles/git/gitconfig` (the only file that is
  copied rather than symlinked).
* You want to pull changes from the remote repository.
* You want to update Homebrew formulae and Node packages.

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

### Automatic software installation

Homebrew formulae:

* GNU core utilities
* [git](http://git-scm.com/)
* [ack](http://betterthangrep.com/)
* bash (latest version)
* [bash-completion](http://bash-completion.alioth.debian.org/)
* [ffmpeg](http://ffmpeg.org/)
* [graphicsmagick](http://www.graphicsmagick.org/)
* [jpeg](https://en.wikipedia.org/wiki/Libjpeg)
* [node](http://nodejs.org/)
* nvm
* [optipng](http://optipng.sourceforge.net/)
* [phantomjs](http://phantomjs.org/)
* [rsync](https://rsync.samba.org/) (latest version, rather than the out-dated OS X installation)
* [tree](http://mama.indstate.edu/users/ice/tree/)
* [wget](http://www.gnu.org/software/wget/)
* Yarn
* zsh
* zsh-completion

Node packages:

* [gify](https://github.com/visionmedia/node-gify)
* [jshint](http://www.jshint.com/)
* [yo](http://yeoman.io/)

### Custom OS X defaults

Custom OS X settings can be applied during the `dotfiles` process. They can
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


### ZSH and oh-my-zsh custom prompts

This can be run with ZSH shell, running an external theme called PowerLevel9k. Ensure you install oh-my-zsh and the theme
to take advantage of the `.zshrc` settings.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
```bash
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```

### Hyper term and configuration

Download the latest version of Hyper to take advantage of the .hyper.js settings

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


## Adding new git submodules

If you want to add more git submodules, e.g., Vim plugins to be managed by
pathogen, then follow these steps while in the root of the superproject.

```bash
# Add the new submodule
git submodule add https://example.com/remote/path/to/repo.git vim/bundle/one-submodule
# Initialize and clone the submodule
git submodule update --init
# Stage the changes
git add vim/bundle/one-submodule
# Commit the changes
git commit -m "Add a new submodule: one-submodule"
```


## Updating git submodules

Updating individual submodules within the superproject:

```bash
# Change to the submodule directory
cd vim/bundle/one-submodule
# Checkout the desired branch (of the submodule)
git checkout master
# Pull from the tip of master (of the submodule - could be any sha or pointer)
git pull origin master
# Go back to main dotfiles repo root
cd ../../..
# Stage the submodule changes
git add vim/bundle/one-submodule
# Commit the submodule changes
git commit -m "Update submodule 'one-submodule' to the latest version"
# Push to a remote repository
git push origin master
```

Now, if anyone updates their local repository from the remote repository, then
using `git submodule update` will update the submodules (that have been
initialized) in their local repository. N.B This will wipe away any local
changes made to those submodules.


## Acknowledgements

Inspiration and code was taken from many sources, including:

* [@mathiasbynens](https://github.com/mathiasbynens) (Mathias Bynens)
  [https://github.com/mathiasbynens/dotfiles](https://github.com/mathiasbynens/dotfiles)
* [@tejr](https://github.com/tejr) (Tom Ryder)
  [https://github.com/tejr/dotfiles](https://github.com/tejr/dotfiles)
* [@gf3](https://github.com/gf3) (Gianni Chiappetta)
  [https://github.com/gf3/dotfiles](https://github.com/gf3/dotfiles)
* [@cowboy](https://github.com/cowboy) (Ben Alman)
  [https://github.com/cowboy/dotfiles](https://github.com/cowboy/dotfiles)
* [@alrra](https://github.com/alrra) (Cãtãlin Mariş)
  [https://github.com/alrra/dotfiles](https://github.com/alrra/dotfiles)
