# Setting up a fresh Windows machine

## TODO

- [ ] evaluate [Boxstarter](http://boxstarter.org/) (see blog post by jsfraz: [Setting Up a Windows Machine in a Reproducible Way](https://blog.jessfraz.com/post/windows-for-linux-nerds/#setting-up-a-windows-machine-in-a-reproducible-way))

## Chocolatey

### First Time Setup

- [install Chocolatey](https://chocolatey.org/install) as described (from Admin `cmd` or `PowerShell`)
- `choco` should be in `%PATH%` after installation
  - ProTip™: use `which` npm package (`npm install -g which`)

### Usage

It makes sense to always use an elevated (Admin) `cmd` or `PowerShell` to work with `choco` (as we are installing software, this is perfectly fine.)

To install something new:

- `choco search foo`
- `choco install foo`

List and upgrade locally installed packages.

- `choco list -l`
- `choco upgrade all`

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
  - symlink `WinCompose.XCompose` to `.XCompose` in `%userprofile%` (details how to symlink are at the top of `WinCompose.XCompose` itself)
  - use a env clone in Windows for this; do not link to env within WSL!

## System Tools

### Link Shell Extension

[Link Shell Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html) - to create
symlinks, hardlinks, junctions, etc.

### clink

[clink](https://mridgers.github.io/clink/) - readline/history for `cmd.exe`

- symlink `env/clink/settings` to `C:\Users\<USERNAME>\AppData\Local\clink`
- create *hardlink* to `env/.inputrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.inputrc` to `_inputrc`
- edit shipped configuration: `C:\Program Files (x86)\clink\<VERSION>\clink_inputrc_base`
- comment out those lines: `#M-h: show-rl-help`

### ConsoleZ

[ConsoleZ](https://github.com/cbucher/console) - a proper terminal around `cmd` and `PowerShell`

Settings are stored in `%APPDATA%\Console`, e.g.
`C:\Users\yogan\AppData\Roaming\Console`.

### Miscellaneous

- [Process Explorer](https://technet.microsoft.com/en-us/sysinternals/bb896653.aspx)
- [Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902.aspx)

## Applications

### Vim

- [Download Windows Installer](http://www.vim.org/download.php#pc) and run it
- create *hardlink* to `env/.vimrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.vimrc` to `_vimrc`
- make *junction* of `env/.vim/` to `c:\Program Files\vim\`
- rename `.vim` to `vimfiles` (remove old one there)

### Spotify

- [Spotify](https://www.spotify.com)
- [Toastify](https://toastify.codeplex.com/) - global keyboard shortcuts and notifications

### Graphics/Viewers

- [Paint.NET](http://www.getpaint.net)
- [Greenshot](http://getgreenshot.org/de/)
- [ScreenToGif](http://www.screentogif.com/)
- [SumatraPDF](http://www.sumatrapdfreader.org/free-pdf-reader.html)

## Cygwin/Babun

**TODO:** *Remove this section, refer to [WSL](wsl.md) instead. Decide where to document cloning of env (short version: one clone in WLS, one in Windows home, b/c file i/o)*

[Babun](https://babun.github.io)

### mintty

- `ln -s env/.minttyrc`
- change taskbar icon to call:
  - `mintty.exe /bin/zsh --login`

### Symlinks

```sh
ln -s /cygdrive/c
ln -s c/Users/yogan winhome
```

### Clone git Repos

Since the whole cygwin/Babun dir tree is somehow fucked up regarding default permissions,
clone all git repos into Windows home, and symlink to them from within cygwin
for quick access.

```sh
cd winhome
git clone ssh://zogan.de/~yogan/git/priv/env
git clone ssh://zogan.de/~yogan/git/priv/docs
cd ; ln -s winhome/env ; ln -s winhome/docs
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

Settings are stored in `%APPDATA%\Code\User\`.

**TODO:** *figure out how this fscking `syncLocalSettings.json` works*

## References

- [SoCraTes 2016 Windows Tools Session Notes](https://blog.sandra-parsick.de/2016/09/20/summary-of-socrates-2016-session-hey-dude-where-is-my-tool-chain-working-on-windows-as-a-linux-user-aka-lets-talk-about-windows/)
