# Installation — instructions prepared for the first beta

The first beta is not published yet. WinGet and APT commands below become usable
only after the corresponding channel is announced as available.

## Windows x64

Download the official `*-setup.exe` from this repository's Releases and double-click
it. The installer includes CLI, GUI and capture components. Windows can request
administrator authorization for the capture service. Launch Proxyrun from Start;
open a new terminal to use `prun` or `proxyrun`.

After WinGet acceptance:

```powershell
winget install --id RodionMasalov.Proxyrun -e
winget upgrade --id RodionMasalov.Proxyrun -e
```

The earlier ZIP preview uses a different installer. Close owned launches and
uninstall that preview with its `install.cmd -Uninstall` before installing the new
package. Profiles are preserved. Do not remove profile files manually.

## Ubuntu 24.04 amd64 / Ubuntu 24.04 in WSL 2

Once the signed APT repository is published, add its dedicated public key and
source, then install `proxyrun-gui`. It depends on the CLI package `proxyrun`.
The repository supplies only these packages. It does not replace OS libraries.

Download `apt/proxyrun-archive-keyring.gpg`, `apt/proxyrun.sources` and
`apt/proxyrun.pref` from the official release website. Check the announced key
fingerprint. Install the public key as
`/usr/share/keyrings/proxyrun-archive-keyring.gpg`, the source as
`/etc/apt/sources.list.d/proxyrun.sources`, and the preferences as
`/etc/apt/preferences.d/proxyrun.pref`.

```bash
sudo apt update
sudo apt install proxyrun-gui
```

CLI only: `sudo apt install proxyrun`. Upgrade with the normal APT workflow.
Profiles remain in the user's configuration directory when packages are removed.
The package does not start a root-owned copy of the user's daemon during dpkg
installation. CLI launches start the user daemon when needed; saved Auto proxy
rules start in an XDG graphical login session. WSL without WSLg supports CLI use;
GUI use requires WSLg and its Linux runtime dependencies.

Linux/WSL packages target Linux programs. Install the native Windows version to
proxy Windows applications. Native Ubuntu and WSL require separate compatibility
checks; a passing packaging test is not a capture test.
