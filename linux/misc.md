# Linux

## bat - cat Replacement

`bat` works like `cat`, but adds some comfort features like syntax
highlighting, automatic paging, and a git diff column.

* install latest `*_amd64.deb` from
  [GitHub releases](https://github.com/sharkdp/bat/releases)

## progress - Coreutils Progress Viewer

Nice command line tool to watch the progress of copy-like programs like
`cp`, `mv`, `dd`, `gzip`, `cat`, etc. It works be scanning `/proc` and
analyzing `fd` and `fdinfo` files for relevant processes.

### Install

* clone [GitHub repo](https://github.com/Xfennec/progress):
  `git clone https://github.com/Xfennec/progress.git`
* `make && make install`

### Usage

* top-like watcher mode: `progress -M` (will just magically detect
  interesting processes and show their progress)
* for other modes (restrict to process with PID or command names),
  see `progress -h`

## Fonts

### Installing custom fonts

Current user:

* `cp foo.ttf ~/.local/share/fonts/`
* subdirs are also fine, e.g. `~/.local/share/fonts/NerdFonts/`

System wide

* `cp foo.ttf /usr/share/fonts/truetype/…`

List installed fonts

* `gnome-font-viewer`

### Using patched NerdFonts with urxvt

* download "DejaVu Sans Mono Nerd Font" from [NerdFonts
  repo](https://github.com/ryanoasis/nerd-fonts/releases)
* `cp *Mono.ttf ~/.local/share/fonts/NerdFonts/`
* `vim ~/.Xdefaults`

```Xdefaults
URxvt.font:     xft:DejaVuSansMono Nerd Font Mono-10
URxvt.boldFont: xft:DejaVuSansMono Nerd Font Mono-10:bold
```
