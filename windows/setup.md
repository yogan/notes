# Setting up a fresh Windows machine

## Chocolatey

### First Time Setup

- [install Chocolatey](https://chocolatey.org/install) as described (from Admin
  `cmd` or `PowerShell`)
- `choco` should be in `%PATH%` after installation
  - ProTip™: use `which` npm package (`npm install -g which`)
- `choco feature enable -n=allowGlobalConfirmation`

### Usage

It makes sense to always use an elevated (Admin) `cmd` or `PowerShell` to work
with `choco` (as we are installing software, this is perfectly fine.)

To install something new:

- `choco search foo`
- `choco install foo`

List and upgrade locally installed packages.

- `choco list -l`
- `choco upgrade all`

## Essentials

- [Chrome](https://www.google.de/intl/de/chrome/browser/desktop/index.html) -
  `choco install GoogleChrome`
- [Dropbox](http://www.dropbox.com) - `choco install dropbox`, get `keepass.db`
- [Keepass](http://keepass.info/) - `choco install keepass`

## Keyboard

- [SharpKeys](https://sharpkeys.codeplex.com) - `choco install sharpkeys`
  - map `<CapsLock>` → `<Ctrl>`
  - swap `<Esc>` ↔ `<~>`
- [WinCompose](https://github.com/SamHocevar/wincompose) - `choco install wincompose`
  - symlink `WinCompose.XCompose` to `.XCompose` in `%userprofile%` (details how
    to symlink are at the top of `WinCompose.XCompose` itself)
  - use a env clone in Windows for this; do not link to env within WSL!

## System Tools

### Link Shell Extension

[Link Shell
Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html) -
`choco install LinkShellExtension` - to create symlinks, hardlinks, junctions,
etc.

### clink

[clink](https://mridgers.github.io/clink/) - `choco install clink` -
readline/history for `cmd.exe`

- symlink `env/clink/settings` to `C:\Users\<USERNAME>\AppData\Local\clink`
- create *hardlink* to `env/.inputrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.inputrc` to `_inputrc`

Those steps seem no longer necessary (check if the `meta+h` binding from
`.inputrc` is working):

- ~~edit shipped configuration: `C:\Program Files (x86)\clink\<VERSION>\clink_inputrc_base`~~
- ~~comment out those lines: `#M-h: show-rl-help`~~

### ConsoleZ

[ConsoleZ](https://github.com/cbucher/console) - `choco install ConsoleZ` - a
proper terminal around `cmd` and `PowerShell`

Settings are stored in `%APPDATA%\Console`, e.g.
`C:\Users\yogan\AppData\Roaming\Console`.

### Miscellaneous

- [Process
  Explorer](https://technet.microsoft.com/en-us/sysinternals/bb896653.aspx) -
  `choco install procexp`
- [Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902.aspx) -
  `choco install AutoRuns`

## Applications

### Vim

- `choco install vim`
- create *hardlink* to `env/.vimrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.vimrc` to `_vimrc`
- make *junction* of `env/.vim/` to `c:\Program Files\vim\`
- rename `.vim` to `vimfiles` (remove old one there)

### Spotify

- [Spotify](https://www.spotify.com) - `choco install spotify`
- [Toastify](https://toastify.codeplex.com/) - `choco install toastify` - global
  keyboard shortcuts and notifications

### Graphics/Viewers

- [SumatraPDF](http://www.sumatrapdfreader.org/free-pdf-reader.html) -
  `choco install sumatrapdf`
- [Paint.NET](http://www.getpaint.net) - `choco install paint.net`
- [Greenshot](http://getgreenshot.org/de/) - `choco install greenshot`
- [ScreenToGif](http://www.screentogif.com/) - `choco install screentogif`
- also see [tools/graphics page](../tools/graphics.md)

## WSL

See [Windows Subsystem for Linux (WSL)](wsl.md).

### Clone git Repos

To enable working with both Linux (WSL) and Windows programs on the files in my
git repositories, they have to be cloned to a Windows path. Cloning and other
git operations can be done straight from a WSL shell with WSL git.

```sh
cd winhome
git clone ssh://zogan.de/~yogan/git/priv/env
git clone ssh://zogan.de/~yogan/git/priv/docs
cd ; ln -s winhome/env ; ln -s winhome/docs
```

## Development

### VS Code

- `choco install VisualStudioCode`
- be sure to have Explorer integration checked (if not, run installer again
  later)

For initial setup, get user settings from gist:

- add the [Settings
  Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)
  extension
- `<Ctrl><Shift><p>` → `Preferences: Open User Settings`
  - add `"sync.gist": "ae3bdfbb98c2054b242e1e0361628bfb"`
  - remove all other `sync.*` settings
- `<Ctrl><Shift><p>` → `Sync: Download settings`

Settings are stored in `%APPDATA%\Code\User\`.

**TODO:** *figure out how this fscking `syncLocalSettings.json` works*

## References

- [SoCraTes 2016 Windows Tools Session Notes](https://blog.sandra-parsick.de/2016/09/20/summary-of-socrates-2016-session-hey-dude-where-is-my-tool-chain-working-on-windows-as-a-linux-user-aka-lets-talk-about-windows/)

## TODO

- [ ] evaluate [Boxstarter](http://boxstarter.org/) (see blog post by jsfraz:
  [Setting Up a Windows Machine in a Reproducible
  Way](https://blog.jessfraz.com/post/windows-for-linux-nerds/#setting-up-a-windows-machine-in-a-reproducible-way))
