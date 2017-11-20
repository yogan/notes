# Searching

## ripgrep (`rg`)

[ripgrep](https://github.com/BurntSushi/ripgrep)
is an even faster alternative to `grep` then `ack` or `ag` (by giving up advanced regex features like look-behind).

### Installation

* download pre-built tarball (`ripgrep-0.7.1-i686-unknown-linux-musl.tar.gz`) from [GitHub releases](https://github.com/BurntSushi/ripgrep/releases)
* `xtract.sh ripgrep*tar.gz ; cd ripgrep*`
* `cp rg ~/local/bin/`
* `cp rg.1 ~/local/share/man/man1/`

### Fish completion

This is already in `env` with modifications (support for `rgl` rg+less wrapper). Merge upstream versions when needed:

`vimdiff complete/rg.fish ~/.config/fish/completions/rg.fish`
