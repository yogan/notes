# fish Shell

- [Documentation](https://fishshell.com/docs/current/index.html)
- [GitHub page](https://github.com/fish-shell/fish-shell/)

## Build and Install from Source

* `git clone git://github.com/fish-shell/fish-shell.git && cd fish-shell`
* `sudo apt install autoconf automake build-essential libncurses5-dev gettext doxygen`
* `autoreconf --no-recursive`

### Linux

* `./configure --prefix=$HOME/local`
* `make && make install` *(maybe add `-j` to `make` if running on a juicy machine)*
* add `$HOME/local/bin/fish` to `/etc/shells`
* `chsh -s $HOME/local/bin/fish`

### WSL

* `./configure` *(it's fine to install globally)*
* `make && sudo make install` *(maybe add `-j` to `make` if running on a juicy machine)*
* see [terminal section on WSL page](../windows/wsl.md#add-minttywsltty-as-terminal) on how to launch WSL with a custom shell

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
