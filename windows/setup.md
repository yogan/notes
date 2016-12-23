# Setting up a fresh Windows machine

## Essentials
* [Chrome](https://www.google.de/intl/de/chrome/browser/desktop/index.html)
* [Dropbox](http://www.dropbox.com)
  * install client, get `keepass.db`
* [Keepass](http://keepass.info/)


## Keyboard
* [SharpKeys](https://sharpkeys.codeplex.com)
  * map `<CapsLock>` → `<Ctrl>`
  * swap `<Esc>` ↔ `<~>`
* [WinCompose](https://github.com/SamHocevar/wincompose)


## System Tools

### Link Shell Extension
[Link Shell Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html) - to create symlinks/hardlinks/other magic

### clink
[clink](https://mridgers.github.io/clink/) - readline/history for `cmd.exe`

* symlink `env/clink/settings` to `C:\Users\<USERNAME>\AppData\Local\clink`
* create **hardlink** to `env/.inputrc` in `$HOME` (`c:/user/foo/`)
* rename hardlinked `.inputrc` to `_inputrc`
* edit shipped configuration: `C:\Program Files (x86)\clink\<VERSION>\clink_inputrc_base`
* comment out those lines:  
`#M-h:                show-rl-help`

### ConsoleZ
[ConsoleZ](https://github.com/cbucher/console)

Settings are stored in `%APPDATA%\Console`, e.g.
`C:\Users\yogan\AppData\Roaming\Console`.  
Symlink config from env there.


## Applications

### Vim
* [Download Windows Installer](http://www.vim.org/download.php#pc) and run it
* create **hardlink** to `env/.vimrc` in `$HOME` (`c:/user/foo/`)
* rename hardlinked `.vimrc` to `_vimrc`
* make **junction** of `env/.vim/` to `c:\Program Files\vim\`
* rename `.vim` to `vimfiles` (remove old one there)

### Spotify
* [Spotify](https://www.spotify.com)
* [Toastify](https://toastify.codeplex.com/) - global keyboard shortcuts and notifications

## Cygwin/Babun
[Babun](https://babun.github.io)

### mintty
* `ln -s env/.minttyrc`
* change taskbar icon to call:
	* `mintty.exe --config ~/.minttyrc /bin/env MINTTY_THEME=black /bin/zsh --login`

### Symlinks
```
$ ln -s /cygdrive/c
$ ln -s c/Users/yogan winhome
```

### Clone git Repos
Since the whole cygwin/Babun dir tree is somehow fucked up regarding permissions,
clone all git repos into Windows home, and rather symlink to them from within cygwin
for easy access.
```
$ cd winhome
$ git clone ssh://zogan.de/~yogan/git/priv/env
$ git clone ssh://zogan.de/~yogan/git/priv/docs
$ cd ; ln -s winhome/env ; ln -s winhome/docs
```

## References
* [SoCraTes 2016 Windows Tools Session Notes](https://blog.sandra-parsick.de/2016/09/20/summary-of-socrates-2016-session-hey-dude-where-is-my-tool-chain-working-on-windows-as-a-linux-user-aka-lets-talk-about-windows/)