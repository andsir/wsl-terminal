# wsl-terminal

A terminal emulator for Windows Subsystem for Linux (WSL), includes [mintty](http://mintty.github.io/), [wslbridge](https://github.com/rprichard/wslbridge), [cbwin](https://github.com/xilun/cbwin), and some other useful tools.

## Screenshot

![screenshot](https://raw.githubusercontent.com/wiki/goreliu/wsl-terminal/images/wsl-terminal-3.png)

[More screenshots.](https://github.com/goreliu/wsl-terminal/wiki/Screenshots)

## Usage

1. [Download here.](https://github.com/goreliu/wsl-terminal/releases)

2. Run `open-wsl.exe` to open a WSL terminal in current directory (need to be on a local NTFS volume, [more details](https://github.com/rprichard/wslbridge)).

3. Run `tools/add-open-wsl-here-menu.js` to add a `Open WSL Here` context menu to explorer.exe (run `tools/remove-open-wsl-here-menu.js` to remove it). If you are using Total Commander, read [Use wsl-terminal with Total Commander](https://github.com/goreliu/wsl-terminal/wiki/Use-wsl-terminal-with-Total-Commander).

4. `run-wsl-file.exe` can run any `.sh` (and any others like `.py/.pl/.php`) script files in wsl-terminal, support `Open With` context menu in explorer.exe.

5. `vim.exe` can open any files in vim (in wsl-terminal), support `Open With` context menu in explorer.exe. `vim.exe` can be renamed to `emacs.exe/nvim.exe/nano.exe/less.exe/...` to open files in `emacs/nvim/nano/less/...`.

## Configuration files

`etc/wsl-terminal.conf` is wsl-terminal config file.
```
[config]
title="        "
shell=bash
use_cbwin=0
use_tmux=0
;icon=
;distro_guid=
```

`etc/themes/` are theme files, [use themes](https://github.com/goreliu/wsl-terminal/wiki/Use-themes).

`etc/minttyrc` is mintty config file, [mintty tips](https://github.com/mintty/mintty/wiki/Tips).

## Keyboard shortcuts

`Alt + Enter`: Fullscreen

`Alt + F2`: New window

`Alt + F3`: Search text

`Ctrl + [Shift] + Tab`: Switch window

`Ctrl + =+/-/0`: Zoom

`Ctrl + Click`: Open URL or dir/file under the cursor

## Params

```
Usage: open-wsl [OPTION]...
  -a: activate an existing wsl-terminal window, if use_tmux=1, attach the running tmux session.
  -l: start terminal in your home directory (doesn't work with tmux).
  -C dir: change directory to dir.
  -d distro: switch distros.
  -b "options": pass additional options to wslbridge.
  -h: show help.
```

See also [mintty params](https://github.com/goreliu/wsl-terminal/wiki/mintty-params) and [wslbridge params](https://github.com/rprichard/wslbridge#usage).

## Switch distros

Use `open-wsl -d distro` to switch distros:

```
# list all distros
> wslconfig /l
Legacy (Default)
Ubuntu

# use Ubuntu (will run wslconfig /s Ubuntu before mintty)
> open-wsl -d Ubuntu

# Ubuntu is the default distro now
> wslconfig /l
Ubuntu (Default)
Legacy
```

Or set `distro_guid` in wsl-terminal.conf (Won't change the default distro).

Double click `tools/write-distro-guids-to-config-file.js` (If it was open by any editor, open it with `Microsoft (R) Windows Based Script Host`, or open a `cmd.exe` in `tools` directory and run `wscript write-distro-guids-to-config-file.js`).

Then a msgbox will show the result:

```
result has been written to ..\etc\wsl-terminal.conf:

; Legacy
;distro_guid={12345678-1234-5678-0123-456789abcdef}

; Ubuntu
;distro_guid={47a89313-4300-4678-96ae-e53c41a79e03}

remove the ; before distro_guid to use the distro.
```

If you want to pass the distro_guid to open-wsl in cmdline:

```
# pass the distro guid to wslbridge
> open-wsl -b "--distro-guid {47a89313-4300-4678-96ae-e53c41a79e03}"
```

## Links

[FAQ](https://github.com/goreliu/wsl-terminal/wiki/FAQ)

[TODO](https://github.com/goreliu/wsl-terminal/wiki/TODO)

## Build

Make sure `wget/tar/xz/gzip/p7zip` (Ubuntu: run `apt install wget tar xz-utils gzip p7zip-full`, Archlinux: run `pacman -S wget tar xz gzip p7zip`) are installed in WSL.

Run `build.bat`.

## License

[Cygwin DLL](https://www.cygwin.com/): https://cygwin.com/licensing.html

[mintty](http://mintty.github.io/): GPLv3+

[wslbridge](https://github.com/rprichard/wslbridge): MIT

[cbwin](https://github.com/xilun/cbwin): MIT

[wsl-terminal](https://github.com/goreliu/wsl-terminal): MIT
