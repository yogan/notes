# Windows Subsystem for Linux (WSL) aka Bash on Ubuntu on Windows

Ongoing installation/setup notes.

## TODOs
* check why `git` behaves so weird wrt. file permissions (probably due to wrong `umask` [#1801](https://github.com/Microsoft/BashOnWindows/issues/1801), [#352](https://github.com/Microsoft/BashOnWindows/issues/352))

## Resources
* [List blog posts and Channel 9 videos of WSL internals](https://blogs.msdn.microsoft.com/commandline/learn-about-bash-on-windows-subsystem-for-linux/)
* [Microsoft/BashOnWindows GitHub Issue Tracker](https://github.com/microsoft/bashonwindows)
* [List of programs that work on WSL](https://github.com/ethanhs/WSL-Programs) / [Can I Subsystem It?](https://github.com/davatron5000/can-i-subsystem-it)

## Install
* [Installation Guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)
* TL;DR:
  * enable Developer Mode (Settings → Update and Security → For developers)
  * turn it on: Start → "turn feat" → "Turn Windows features on or off" → [x] WSL
  * reboot when prompted
  * `cmd` → `bash` → let installer run
  * `cmd` → `bash` → create user/password

## Post-Install
 * `sudo apt-get dist-upgrade`
 * `sudo install git zsh`
 * `ssh-keygen ; eval $(ssh-agent) ; ssh-add`
 * `git clone ssh://yogan@zogan.de/~yogan/git/priv/env`
 * `./env/bin/symlink-env.sh`
 * `chmod 700 .zsh/ .zsh/functions/`

## Add mintty as Terminal
* [wsltty@GitHub](https://github.com/mintty/wsltty)
* symlink `env/.minttyrc` to `%APPDATA%\mintty\config` (rename `.minttyrc` to `config`)
* copy shortcut in `%APPDATA%\Microsoft\Windows\Start Menu\Programs\WSLtty`
* adapt to use `zsh` instead of `bash`: `%LOCALAPPDATA%\wsltty\bin\mintty.exe -t "wsl/zsh" --wsl /bin/wslbridge -C~ -t /bin/zsh --login`

## zsh
* `compaudit` complained (rightfully) about insecure directories,
  which came from the `git` clone (`.zsh/` and `.zsh/functions/`); `chmod` to something proper…
* workaround to make default shell (`chsh` does not help):
  * launch from `mintty` via `wslbridge` (see above)
  * add `export SHELL=/bin/zsh` to `~/.zshenv`
