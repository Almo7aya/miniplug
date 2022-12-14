> A fork of [miniplug](https://git.sr.ht/~yerinalexey/miniplug/)


# Miniplug
Minimalistic plugin manager for ZSH.

It was developed as a drop-in replacement for [zplug](https://github.com/zplug/zplug) and [Antigen](https://github.com/zsh-users/antigen). They both have serious problems and are not maintained anymore.

# Features
- No crashes or double plugin loading when re-sourcing `.zshrc`
- Unlike [Antigen](https://github.com/zsh-users/antigen), Miniplug does not pollute your `$PATH`
- Only bare minimum for managing plugins

# Requirements
- ZSH
- Git
- `awk` (`gawk`)

# Installation
To install Miniplug you need to download [`miniplug.zsh`](./miniplug.zsh) file and source it in your `.zshrc`:
```sh
# Download miniplug:
git clone https://github.com/Almo7aya/miniplug $HOME/.local/share/miniplug

# Add to zshrc:
source "$HOME/.local/share/miniplug/miniplug.zsh"
```
> You can download this file anywhere, `$HOME/.local/share/miniplug/miniplug.zsh` is just an example

# Usage
After `miniplug.zsh` file is sourced, you'll get access to `miniplug` CLI
utility. Define plugins using `miniplug plugin <URL>`. Or define a theme using
`miniplug theme <URL>` (theme can be set only once)
> `<URL>` can be URL to Git repo or Github's `user/repo`

After plugins are defined, you can download them using `miniplug install` and
source them using `miniplug load` (should be added to `.zshrc`).

## Example `.zshrc`:
```sh
source "$HOME/.local/share/miniplug/miniplug.zsh"

# Define a plugin
miniplug plugin 'zsh-users/zsh-syntax-highlighting'

# Define a theme
miniplug theme 'dracula/zsh'

# Source plugins
miniplug load
```

## Changing plugin folder
Plugins will be downloaded to `$XDG_DATA_HOME/miniplug` (or `~/.local/share/miniplug` if not set)
by default. To change that location, set `MINIPLUG_HOME` environment variable
to a new path:
```sh
export MINIPLUG_HOME="$HOME/.config/zsh/plugins"
```

## Updating plugins
To update plugins you can run:
```sh
miniplug update
```

If you want to force plugin not to update, you can detach repo's `HEAD` by running this snippet in plugin folder (`$MINIPLUG_HOME/user/repo`):
```sh
git checkout "$(git log --format=%H | head -1)"
```

After that, plugin will be skipped when you run `miniplug update`

# License
[Apache 2.0](./LICENSE)
