# fish Shell

* [Documentation](https://fishshell.com/docs/current/index.html)
* [GitHub page](https://github.com/fish-shell/fish-shell/)

## Build and Install from Source

### Get Source

* get tarball from [GitHub Releases](https://github.com/fish-shell/fish-shell/releases)
* `sudo apt install build-essential cmake ncurses-dev libncurses5-dev libpcre2-dev gettext`

### Configure with CMake

Preferred, but needs CMake ≥ 3.2 (not in Debian Jessie).

* `mkdir build ; cd build`
* `cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local ..`
  * prefix optional, depending on where you want to have fish installed to

### Configure with autotools

* `autoreconf --no-recursive`
  * if building from Git
* `./configure --prefix=$HOME/local`
  * prefix optional, depending on where you want to have fish installed to

### Build and Install

* `make && make install`
  * maybe add `-j` to `make` if running on a juicy machine
  * `make install` might need `sudo`, depending on the configured install target dir

## Set fish as default user shell

* `sudo sh -c 'echo $(which fish) >> /etc/shell`
* `chsh -s $(which fish)`

## Get dotfiles ready

* `cd ~/.config`
* `ln -s ~/env/.config/fish`
* `ln -s ~/env/.config/omf`

## Setup $PATH / $fish_user_paths

Path things are a bit weird in fish. You can add paths to a universal variable
`fish_user_paths`, which then magically is persisted on the local machine, and
also prepended to `PATH`. This actually works better then expected. I have two
little convenience functions `path` (to print the values of the two variables)
and `add_path` (to add e.g. `~/bin`, `~/.fzf/bin`, etc.)

One thing to absolutely add is the path to the fish binary itself, i.e.
`add_path $HOME/local/bin`.

## Setup oh-my-fish

* `curl -L https://get.oh-my.fish | fish` (if you like to live dangerously, or
  [download and check](https://github.com/oh-my-fish/oh-my-fish#installation)
  the installer first)
* `omf install` (to get theme)
* `omf reload`

## Setup fzf

* `git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf`
* `~/.fzf/install`
* answer setup questions:
  * `Do you want to enable fuzzy auto-completion?` **`y`**
  * `Do you want to enable key bindings?`  **`y`**
  * `Do you want to update your shell configuration files?` **`n`**
* `omf reload`
