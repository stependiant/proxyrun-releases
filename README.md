# Proxyrun - per-app proxy for Windows and Linux

Proxyrun is a **free per-application proxy client** for Windows and Linux / WSL.
Route browsers, desktop applications and command-line tools through your own
**HTTP, HTTPS or SOCKS5** proxy. Choose a different proxy profile for each application.
All current features are free: CLI, desktop UI, profiles and Auto proxy.
Bring your own proxy server; no Proxyrun account is required. Future proxy purchases
or subscriptions will be optional. Proxyrun is an independent application.

[Website and downloads](https://stependiant.github.io/proxyrun-releases/) ·
[Wiki and user guide](https://stependiant.github.io/proxyrun-releases/wiki/)

**0.1.0-beta.3 - Windows x64 and Ubuntu 24.04 amd64 / WSL 2.**
Download installers from Releases or use the signed APT repository. WinGet is not
available yet. This beta's Windows installer is unsigned.
Beta 2 users upgrade through Setup or APT. After installing beta 3, Proxyrun can
report and install future updates on request.

## Use cases

| Task | How Proxyrun helps |
| --- | --- |
| Launch a browser or command-line tool through a proxy | Start an installed application with the selected HTTP, HTTPS or SOCKS5 profile. |
| Give different apps different proxies | Assign a profile to each saved application, or use a shared default. |
| Proxy apps opened from normal OS shortcuts | Enable Auto proxy for the executable and wait for the rules to apply. |
| Use the same proxy setup in a GUI and terminal | The desktop app, `prun` and `proxyrun` share profiles. |

## How to use Proxyrun

1. Install Proxyrun and open **Profiles**.
2. Add your proxy server address, port, protocol and optional credentials.
3. Save it and click **Check connection**.
4. Open **Applications**, choose an app and click **Launch**.

Use the pencil button on an application to choose its **Proxy profile**.
**Use default profile** follows the star-marked profile in Profiles.
Enable **Auto proxy** if you want the application to use the proxy when opened
from its usual OS shortcut; wait for the rules to apply and restart the app.

In a terminal, create a profile with `prun configure`, then launch an
installed app with `prun chrome` or `prun run --profile work chrome`.
`prun` and `proxyrun` share settings with the desktop app.

[Read the Wiki](https://stependiant.github.io/proxyrun-releases/wiki/) ·
[User guide on GitHub](USER-GUIDE.md) ·
[Report a bug](https://github.com/stependiant/proxyrun-releases/issues/new)

## Download

Download from [Releases](https://github.com/stependiant/proxyrun-releases/releases/tag/v0.1.0-beta.3):

| Platform | File | Includes |
| --- | --- | --- |
| Windows x64 | `Proxyrun-Windows-x64-Setup.exe` | Desktop UI and CLI; optional capture-service setup |
| Ubuntu 24.04 / WSL 2, amd64 | `proxyrun_<version>_amd64.deb` | CLI |
| Ubuntu 24.04 / WSL 2, amd64 | `proxyrun-gui_<version>_amd64.deb` | Desktop UI; also requires the CLI package |

[Installation instructions](INSTALL.md) · [Report a bug](https://github.com/stependiant/proxyrun-releases/issues)

WSL packages run Linux applications. The UI requires WSLg.
Use the Windows installer for Windows applications.
Auto proxy may require administrator approval. If system capture stops,
applications can use ordinary system routing; there is no persistent system kill switch.

Application source is private. This repository contains downloads and documentation.
[Third-party licenses and sources](https://stependiant.github.io/proxyrun-releases/third-party/0.1.0-beta.3/proxyrun-third-party-0.1.0-beta.3.tar.gz)
are provided separately and retain their own licenses. Proxyrun uses the
[Proxyrun Freeware License](LICENSE): official binaries are free for personal and
commercial use, including all existing features. Unmodified official installers
may be redistributed without charge with their notices. Previously distributed
beta 1 copies retain their [original MIT terms](licenses/Proxyrun-MIT-beta1.txt).

Contact: rodionmasalov34@gmail.com. Do not include proxy passwords or tokens in issues.

[Changes](CHANGELOG.md) · [Privacy](PRIVACY.md) · [Application license](LICENSE)
