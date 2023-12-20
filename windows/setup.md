# Setting up a fresh Windows machine

## Bootstrapping with Scoop and winget

This works fine for Windows 11, where Windows Terminal and winget are already included.

- [Google Drive](https://www.google.com/drive/download/) (no scoop/winget)
- install [Scoop](https://scoop.sh/) itself (non admin PowerShell):
  - `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`
  - `irm get.scoop.sh | iex`
- git gud: `scoop install git`
- add buckets: `scoop bucket add extras`, `scoop bucket add sysinternals`
- get the goods: `scoop install sharpkeys wincompose clink neovim bat less fd ripgrep keepassxc autoruns processhacker eartrumpet mpv.net paint.net screentogif shutup10 oh-my-posh git-aliases fzf psfzf zlocation`
- software with auto-updates (VS Code, Spotify, PowerToys, Windows Terminal) is better not installed via scoop
- for things that require admin, e.g. OpenVPN:
  - `scoop install sudo`
  - `sudo scoop install openvpn` _yes, sudo in PowerShell \o/_
- remaining stuff with winget:  
  `foreach ($app in @("HermannSchinagl.LinkShellExtension")) { winget install -s winget %app }`

## Updating PowerShell (`pwsh`) and Windows Terminal with Scoop

Since `scoop` is using `pwsh` internally, you will get errors about running `pwsh` processes.
To fix this, start a *Windows PowerShell* (`powershell.exe`) session in Windows Terminal and do `scoop update pwsh` there (see https://github.com/ScoopInstaller/Main/issues/3572#issuecomment-1292873053).

Similar problem for *Windows Terminal*: here, closing all Windows Terminal instances,
starting `conhost` (legacy Windows command prompt), and running 
`scoop update windows-terminal` there is the solution.

## Git

- Git - `winget install -s winget git` / `scoop install git`
- clone dotfiles once for Windows (later again for WSL)
  - in Windows home (`C:\Users\<user>`)
  - `git clone ssh://yogan@zogan.de/~yogan/git/priv/env`

## Keyboard

- [SharpKeys](https://www.randyrants.com/category/sharpkeys/) - `winget install -s winget sharpkeys` / `scoop install sharpkeys`
  - map `<CapsLock>` → `<Ctrl>`
  - swap `<Esc>` ↔ `<~>`
  - *note: PowerToyes has a Keyboard Manager, but that one needs to be running for the
    mappings to work, and generally does not work for some elevated stuff, like win logon;
    SharpKeys does some registry stuff that is lower level and works better*
- [WinCompose](https://github.com/SamHocevar/wincompose) - `winget install -s winget wincompose` / `scoop install wincompose`
  - symlink `WinCompose.XCompose` to `.XCompose` in `%userprofile%` (details how
    to symlink are at the top of `WinCompose.XCompose` itself)
  - use a env clone in Windows for this; do not link to env within WSL!

## System Tools

### Link Shell Extension

[Link Shell
Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html) -
`winget install -s winget HermannSchinagl.LinkShellExtension` - to create symlinks, hardlinks, junctions,
etc.

### clink

[clink](https://chrisant996.github.io/clink/) - `winget install -s winget chrisant996.Clink` -
readline/history for `cmd.exe`

- symlink `env/clink/settings` to `C:\Users\<USERNAME>\AppData\Local\clink\`
- create *hardlink* to `env/.inputrc` in `C:\Users\<USERNAME>\`
- rename hardlinked `.inputrc` to `_inputrc`

### PowerShell

- `winget install -s winget powershell` to install a recent PowerShell
- prompt and keybindings (incl. ^W/^U etc.) are all in `Profile.ps1`
- follow instructions in `env/PowerShell/Profile.ps1`
- `^R` requires `fzf`, which is not available via winget
   - either use `choco` if available, or
   - grab the zipfile from the [GitHub releases](https://github.com/junegunn/fzf/releases)
     - unzip to e.g. `C:\Program Files\Fzf`
     - add that to `$PATH` (system env vars)

### Miscellaneous

- [NanaZip](https://github.com/M2Team/NanaZip) 7zip clone with Win11 integration
- [O&O ShutUp10++](https://www.oo-software.com/en/shutup10) -
  `winget install shutup10++` (available from cmd/PS with `shutup10` after installation)  
  disable a lot of the dubious privacy-violating stuff of Windows 10/11
- [Process Hacker](https://processhacker.sourceforge.io/) -
  `choco install processhacker`  
  seems superior to Process Explorer; last release (2.39) is kinda old (2016),
  project seems to be currently developed as
  [System Informer](https://github.com/winsiderss/systeminformer).
- [Process
  Explorer](https://technet.microsoft.com/en-us/sysinternals/bb896653.aspx) -
  `choco install procexp`
- [TCPView](https://learn.microsoft.com/en-us/sysinternals/downloads/tcpview) -
  `choco install tcpview`
- [Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902.aspx) -
  `choco install AutoRuns`
- [EarTrumpet](https://github.com/File-New-Project/EarTrumpet) -
  `winget install -s winget eartrumpet`  
  nice replacement for Windows volume control/mixer (directly shows controls
  and current volume level of applications)  
- [Rufus](http://rufus.akeo.ie) create bootable USB drives from `.iso` images
  (like with `dd` on Linux) `choco install rufus` (note: `rufus.exe` can be
  found in `C:\ProgramData\chocolatey\bin`, it does not get added to the start
  menu automatically by choco)

## Applications

### Audio / Video

- [Spotify](https://www.spotify.com/de/download/windows/) (winget borken, use installer)
- [Toastify](https://github.com/aleab/toastify/releases) (no winget, use installer) -
  global keyboard shortcuts and notifications
- [mpv.net](https://github.com/stax76/mpv.net) - `winget install -s winget mpv.net`

### Graphics / Document Viewers

- [SumatraPDF](http://www.sumatrapdfreader.org/free-pdf-reader.html) -
  `choco install sumatrapdf`
- [Paint.NET](http://www.getpaint.net) - `choco install paint.net`
- [ScreenToGif](http://www.screentogif.com/) - `winget install -s winget ScreenToGif`
- also see [tools/graphics page](../tools/graphics.md)

### Vim

- `choco install vim`
- create *hardlink* to `env/.vimrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.vimrc` to `_vimrc`
- make *junction* of `env/.vim/` to `c:\Program Files\vim\`
- rename `.vim` to `vimfiles` (remove old one there)

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

### Useful WSL Utilities

- [xclip-xsel-WSL](https://github.com/Konfekt/xclip-xsel-WSL) provides `xclip`
  and `xsel` in WSL so that you can access the Windows clipboard from the
  command line

## Development

### VS Code

- `winget install -s winget vscode`
- enable settings sync (pick everything except UI state), log in via GitHub

## References

- A good starting point for setting up a dev environment on Windows is
  *[Windows development environment](https://docs.microsoft.com/en-us/windows/dev-environment/)*
  on *[Microsoft Docs](https://docs.microsoft.com/en-us/)*.
- [SoCraTes 2016 Windows Tools Session Notes](https://blog.sandra-parsick.de/2016/09/20/summary-of-socrates-2016-session-hey-dude-where-is-my-tool-chain-working-on-windows-as-a-linux-user-aka-lets-talk-about-windows/)

## Package Managers

### Windows Package Manager aka winget (preview)

The
[Windows Package Manager](https://docs.microsoft.com/en-us/windows/package-manager/)
was announced at MS Build 2020 and is currently in preview. It could potentially
replace Chocolatey in the long run. On Windows 10 Insider, `winget` is already
available. For stable Windows 10, the quickest way to get it is to grab the
latest [release from GitHub](https://github.com/microsoft/winget-cli/releases)
(it's part of *AppInstaller*, so download the
`Microsoft.DesktopAppInstaller_GIBBERISH.appxbundle` thingy and run that,
it's fine).

For [winget](https://docs.microsoft.com/en-us/windows/package-manager/winget/)
usage information, just call `winget` without any arguments. There is `search`
and `install`, as you would expect, but currently there does not seem to be an
`update`.

### Chocolatey

#### First Time Setup

- [install Chocolatey](https://chocolatey.org/install) as described (from Admin
  `cmd` or `PowerShell`)
- `choco` should be in `%PATH%` after installation
  - ProTip™: use `which` npm package (`npm install -g which`)
- Run all future `choco` commands as admin
- `choco feature enable -n=allowGlobalConfirmation`

#### Usage

It makes sense to always use an elevated (Admin) `cmd` or `PowerShell` to work
with `choco` (as we are installing software, this is perfectly fine.)

To install something new:

- `choco search foo`
- `choco install foo`

List and upgrade locally installed packages.

- `choco list -l`
- `choco upgrade all`

## TODO

- [ ] evaluate [Boxstarter](http://boxstarter.org/) (see blog post by jsfraz:
  [Setting Up a Windows Machine in a Reproducible
  Way](https://blog.jessfraz.com/post/windows-for-linux-nerds/#setting-up-a-windows-machine-in-a-reproducible-way))
