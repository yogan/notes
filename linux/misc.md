# Linux

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

* download "DejaVu Sans Mono Nerd Font" from [NerdFonts repo](https://github.com/ryanoasis/nerd-fonts/releases)
* `cp *Mono.ttf ~/.local/share/fonts/NerdFonts/`
* `vim ~/.Xdefaults`

```Xdefaults
URxvt.font:     xft:DejaVuSansMono Nerd Font Mono-10
URxvt.boldFont: xft:DejaVuSansMono Nerd Font Mono-10:bold
```