# Install Proxyrun

Beta 0.1.0-beta.3 is available for Windows x64 and Ubuntu 24.04 amd64, including
Ubuntu under WSL 2. Download the installers from
[the beta 3 release](https://github.com/stependiant/proxyrun-releases/releases/tag/v0.1.0-beta.3)
or use the signed APT repository.
The [WinGet submission](https://github.com/microsoft/winget-pkgs/pull/431127) is under review; this version is not available in the catalog yet.

## Windows x64

Download the official `Proxyrun-Windows-x64-Setup.exe` from this repository's Releases and double-click
it. This beta installer is unsigned. If SmartScreen blocks its launch, verify the download against the official release SHA256 before choosing More info, then Run anyway. It includes CLI, GUI and capture components. Windows can request
administrator authorization when you enable the optional capture service from
Applications, then Enable capture service, or run `proxyrun service install`. Setup
registers the desktop, CLI and user startup without requiring this service.
Without the service, instance launches request authorization when needed.
WebView2 is required. Setup downloads Microsoft's official runtime if it is missing, so that first installation needs internet access.
Launch Proxyrun from Start;
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

For a manual installation, download both `.deb` files from the same release, open
a terminal in the download directory and run:

```bash
sudo apt install ./proxyrun_0.1.0-beta.3_amd64.deb ./proxyrun-gui_0.1.0-beta.3_amd64.deb
```

For CLI only, download and install just `proxyrun_0.1.0-beta.3_amd64.deb`.

Add the signed APT repository using its dedicated public key and
source, then install `proxyrun-gui`. It depends on the CLI package `proxyrun`.
The repository supplies only these packages. It does not replace OS libraries.

Run this once to add the repository. The public signing-key
fingerprint is `EC252089E3F4AE497CC0C0483B3CAEC447295DA7`.

```bash
(
set -e
sudo apt update
sudo apt install curl ca-certificates gnupg
proxyrun_setup="$(mktemp -d)"
for file in proxyrun-archive-keyring.gpg proxyrun.sources proxyrun.pref; do
  curl --fail --location "https://stependiant.github.io/proxyrun-releases/apt/$file" \
    --output "$proxyrun_setup/$file"
done
fingerprint="$(gpg --show-keys --with-colons "$proxyrun_setup/proxyrun-archive-keyring.gpg" | awk -F: '$1 == "fpr" { print $10; exit }')"
test "$fingerprint" = EC252089E3F4AE497CC0C0483B3CAEC447295DA7
sudo install -m 644 "$proxyrun_setup/proxyrun-archive-keyring.gpg" /usr/share/keyrings/
sudo install -m 644 "$proxyrun_setup/proxyrun.sources" /etc/apt/sources.list.d/
sudo install -m 644 "$proxyrun_setup/proxyrun.pref" /etc/apt/preferences.d/
sudo apt update
sudo apt install proxyrun-gui
)
```

CLI only: `sudo apt install proxyrun`. Upgrade with the normal APT workflow.
Profiles remain in the user's configuration directory when packages are removed.
The package does not start a root-owned copy of the user's daemon during dpkg
installation. CLI launches start the user daemon when needed; saved Auto proxy
rules start in an XDG graphical login session. WSL without WSLg supports CLI use;
GUI use requires WSLg and its Linux runtime dependencies.

Before removal, close Proxyrun and applications using its proxy sessions, then run
`proxyrun shutdown` as your normal user. Remove the packages with
`sudo apt remove proxyrun-gui proxyrun`. This keeps saved profiles.

Linux/WSL packages target Linux programs. Install the native Windows version to
proxy Windows applications.

## Updating and removing safely

Beta 2 has no built-in updater. To reach beta 3, use the new Windows Setup
with `/UPDATE` or the APT commands below. Keep your existing profiles; no profile
format migration is required. Windows Setup preserves the existing installation
directory, including custom paths with spaces.

After installing beta 3, the desktop can report future updates and install them
when you choose Update now. The CLI commands are `proxyrun update` to check and
`proxyrun update --install` to install. Windows verifies the published installer
size and SHA256 before starting it. Ubuntu requests the exact version through
your configured signed APT repositories. Finish desktop and CLI sessions and
disable Auto proxy first. The updater stops only an idle background service.

Before running Setup manually or removing Proxyrun, close the GUI and desktop-owned launches, disable Auto proxy for saved
applications and run `proxyrun shutdown` when you intend to stop the remaining
Proxyrun sessions. Other programs may depend on these sessions. The installer
refuses running Windows components instead of terminating them. Once those components have stopped, remove Windows Proxyrun through Settings, then Apps. Saved profiles are preserved.

For an in-place Windows update, run the new Setup with `/UPDATE` (add `/S` for
silent installation). WinGet upgrade manifests use this switch. When the optional
capture service is already installed, Setup requests administrator approval to
update its privileged helper too. Uninstalling an earlier beta first also
removes its service; enable it again after reinstalling if needed. Administrator approval
is required to install/update/remove that optional machine service, including uninstall
when it is present. Profiles remain in the user's directory.

On Ubuntu, `sudo apt update && sudo apt upgrade` uses the manually configured
Proxyrun repository. Package scripts do not restart user daemons or proxy
sessions. If an older daemon is still running, Proxyrun reports the version
mismatch and asks you to finish its sessions before restarting it.

Ubuntu 24.04 packages include an AppArmor profile allowing user namespaces for
`/usr/lib/proxyrun/proxyrun` and `/usr/lib/proxyrun/sing-box`. They do not disable
Ubuntu's global restriction. A custom kernel, container or local policy may still
prevent capture. Use `Help & diagnostics` or `proxyrun diagnostics` for component
status; the presence of a profile is not proof that capture works on your system.

## Removing the APT source

Removing Proxyrun packages does not remove a repository you connected manually.
After removing the packages, you can remove these specific repository files:

```bash
sudo rm /etc/apt/sources.list.d/proxyrun.sources
sudo rm /etc/apt/preferences.d/proxyrun.pref
sudo rm /usr/share/keyrings/proxyrun-archive-keyring.gpg
sudo apt update
```

This is Proxyrun's own signed repository. It is not an Ubuntu or Debian official
repository, and its `main` component is only a label inside this repository.
