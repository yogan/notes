# Searching / File Listing

## ripgrep (`rg`)

[ripgrep](https://github.com/BurntSushi/ripgrep) is an even faster alternative
to `grep` then `ack` or `ag` (by giving up advanced regex features like
look-behind).

### Installation

#### Debian Package

* download `.deb` from [GitHub
  releases](https://github.com/BurntSushi/ripgrep/releases)
* `sudo dpkg -i ripgrep_0.8.1_amd64.deb`

#### Manual

* download pre-built tarball (`ripgrep-0.7.1-i686-unknown-linux-musl.tar.gz`)
  from [GitHub releases](https://github.com/BurntSushi/ripgrep/releases)
* `xtract.sh ripgrep*tar.gz ; cd ripgrep*`
* `cp rg ~/local/bin/`
* `cp rg.1 ~/local/share/man/man1/`

### Fish completion

This is already in `env` with modifications (support for `rgl` rg+less wrapper).
Merge upstream versions when needed:

`vimdiff complete/rg.fish ~/.config/fish/completions/rg.fish`

## fd

[`fd`](https://github.com/sharkdp/fd) is the cooler version of `find`
(basically what `rg` is for `grep`).

* TL;DR: use `fd PATTERN` instead of `find -iname '*PATTERN*'`
* output is nicely colored
* respects `.gitignore`, does not include hidden files/dir by default
* smartcase (case insensitive by default, case sensitive when given at least
  one uppercase char)
* regexp, Unicode, and whatnot.

### Installation

Grab the `fd-v*_amd64.db` Debian package from the
[GitHub releases page](https://github.com/sharkdp/fd/releases)
and install with `sudo dpkg -i *.deb` (works just fine on WSL).

### Usage

See `fd -h` or the great [examples on
GitHub](https://github.com/sharkdp/fd#tutorial).

## LSD (LSDeluxe)

[LSD](https://github.com/Peltoche/lsd) is an alternative to `ls` that
adds colors and file type icons (via Nerd Font).

* grab `*_amd64.deb` from the
  [LSD releases](https://github.com/Peltoche/lsd/releases)
* `sudo dpkg -i lsd*.deb`

