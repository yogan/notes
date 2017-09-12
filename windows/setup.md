# Setting up a fresh Windows machine

## TODO
- [ ] try to use [Chocolatey](https://chocolatey.org/) wherever possible
### Choco TL;DR
- start admin PowerShell
- `iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex`
- `choco` should be in `%PATH%` after installation
- still, as software installation usually needs admin rights, call `choco install XYZ` from admin `cmd` or amdin `PowerShell`
- installed software seems to be put to `C:\ProgramData\chocolatey\bin`
	- ProTip™: use `which` from npm package (admin cmd> `npm install -g which`)

## Essentials
- [Chrome](https://www.google.de/intl/de/chrome/browser/desktop/index.html)
- [Dropbox](http://www.dropbox.com)
  - install client, get `keepass.db`
- [Keepass](http://keepass.info/)


## Keyboard
- [SharpKeys](https://sharpkeys.codeplex.com)
  - map `<CapsLock>` → `<Ctrl>`
  - swap `<Esc>` ↔ `<~>`
- [WinCompose](https://github.com/SamHocevar/wincompose)


## System Tools

### Link Shell Extension
[Link Shell Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html) - to create
symlinks, hardlinks, junctions, etc.

### clink
[clink](https://mridgers.github.io/clink/) - readline/history for `cmd.exe`

- symlink `env/clink/settings` to `C:\Users\<USERNAME>\AppData\Local\clink`
- create --hardlink-- to `env/.inputrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.inputrc` to `_inputrc`
- edit shipped configuration: `C:\Program Files (x86)\clink\<VERSION>\clink_inputrc_base`
- comment out those lines:
`#M-h:                show-rl-help`

### ConsoleZ
[ConsoleZ](https://github.com/cbucher/console) - a proper terminal around `cmd` and `PowerShell`

Settings are stored in `%APPDATA%\Console`, e.g.
`C:\Users\yogan\AppData\Roaming\Console`.

### Misc.
- [Process Explorer](https://technet.microsoft.com/en-us/sysinternals/bb896653.aspx)
- [Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902.aspx)


## Applications

### Vim
- [Download Windows Installer](http://www.vim.org/download.php#pc) and run it
- create --hardlink-- to `env/.vimrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.vimrc` to `_vimrc`
- make --junction-- of `env/.vim/` to `c:\Program Files\vim\`
- rename `.vim` to `vimfiles` (remove old one there)

### Spotify
- [Spotify](https://www.spotify.com)
- [Toastify](https://toastify.codeplex.com/) - global keyboard shortcuts and notifications

### Misc.
- [Paint.NET](http://www.getpaint.net)
- [Greenshot](http://getgreenshot.org/de/)
- [ScreenToGif](http://www.screentogif.com/)
- [SumatraPDF](http://www.sumatrapdfreader.org/free-pdf-reader.html)


## Cygwin/Babun

**NOTE:** This can probably soon be completely replaced by [WSL](wsl.md).

[Babun](https://babun.github.io)

### mintty
- `ln -s env/.minttyrc`
- change taskbar icon to call:
	- `mintty.exe /bin/zsh --login`

### Symlinks
```
$ ln -s /cygdrive/c
$ ln -s c/Users/yogan winhome
```

### Clone git Repos
Since the whole cygwin/Babun dir tree is somehow fucked up regarding default permissions,
clone all git repos into Windows home, and symlink to them from within cygwin
for quick access.
```
$ cd winhome
$ git clone ssh://zogan.de/~yogan/git/priv/env
$ git clone ssh://zogan.de/~yogan/git/priv/docs
$ cd ; ln -s winhome/env ; ln -s winhome/docs
```

## Development

### VS Code
- Download [VS Code installer](https://code.visualstudio.com/Download)
- be sure to have Explorer integration checked (if not, run installer again later)

For initial setup, get user settings from gist:
- add the [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) extension
- `<Ctrl><Shift><p>` → `Preferences: Open User Settings`
	- add `"sync.gist": "ae3bdfbb98c2054b242e1e0361628bfb"`
	- remove all other `sync.*` settings
- `<Ctrl><Shift><p>` → `Sync: Download settings`

## References
- [SoCraTes 2016 Windows Tools Session Notes](https://blog.sandra-parsick.de/2016/09/20/summary-of-socrates-2016-session-hey-dude-where-is-my-tool-chain-working-on-windows-as-a-linux-user-aka-lets-talk-about-windows/)
