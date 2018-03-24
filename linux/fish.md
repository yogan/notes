# fish Shell

## Build and Install from Source

* `git clone git://github.com/fish-shell/fish-shell.git && cd fish-shell`
* `sudo apt install autoconf automake build-essential libncurses5-dev gettext doxygen`
* `autoreconf --no-recursive`
* `./configure` *(normally I would add `--prefix=$HOME/local`, but for WSL it's fine to install globally)*
* `make -j && sudo make install`
* *adding to `/etc/shells` and `chsh` are not needed/don't work on WSL*

## Setup oh-my-fish

* `curl -L https://get.oh-my.fish | fish` (if you like to live dangerously, or [download and check](https://github.com/oh-my-fish/oh-my-fish#installation) the installer first)
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

## $PATH / $fish_user_paths

Path things are a bit weird in fish. You can add paths to a universal variable `fish_user_paths`,
which then magically is persisted on the local machine, and also prepended to `PATH`. This actually
works better then expected. I have two little convenience functions `path` (to print the values of
the two variables) and `add_path` (to add e.g. `~/bin`, `~/.fzf/bin`, etc.)