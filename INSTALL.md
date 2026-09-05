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

After publication, run this once to add the repository. The public signing-key
fingerprint is `EC252089E3F4AE497CC0C0483B3CAEC447295DA7`.

```bash
sudo apt update
sudo apt install curl ca-certificates gnupg
proxyrun_setup="$(mktemp -d)"
for file in proxyrun-archive-keyring.gpg proxyrun.sources proxyrun.pref; do
  curl --fail --location "https://stependiant.github.io/proxyrun-releases/apt/$file" \
    --output "$proxyrun_setup/$file" || exit 1
done
fingerprint="$(gpg --show-keys --with-colons "$proxyrun_setup/proxyrun-archive-keyring.gpg" | awk -F: '$1 == "fpr" { print $10; exit }')"
test "$fingerprint" = EC252089E3F4AE497CC0C0483B3CAEC447295DA7 || exit 1
sudo install -m 644 "$proxyrun_setup/proxyrun-archive-keyring.gpg" /usr/share/keyrings/
sudo install -m 644 "$proxyrun_setup/proxyrun.sources" /etc/apt/sources.list.d/
sudo install -m 644 "$proxyrun_setup/proxyrun.pref" /etc/apt/preferences.d/
sudo apt update
sudo apt install proxyrun-gui
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
proxy Windows applications. Native Ubuntu and WSL require separate compatibility
checks; a passing packaging test is not a capture test.
