# Proxyrun

Run applications through your own HTTP, HTTPS or SOCKS5 proxy.
All current features are free: CLI, desktop UI, profiles and Auto proxy.
No account is required. Future proxy purchases or subscriptions will be optional.

**0.1.0-beta.1 is available for Windows x64 and Ubuntu 24.04 amd64 / WSL 2.**
Download installers from Releases or use the signed APT repository. WinGet is not
available yet. This beta's Windows installer is unsigned.

## Download

Download from [Releases](https://github.com/stependiant/proxyrun-releases/releases/tag/v0.1.0-beta.1):

| Platform | File | Includes |
| --- | --- | --- |
| Windows x64 | `Proxyrun-Windows-x64-Setup.exe` | Desktop UI + CLI; automatic capture-service setup |
| Ubuntu 24.04 / WSL 2, amd64 | `proxyrun_<version>_amd64.deb` | CLI |
| Ubuntu 24.04 / WSL 2, amd64 | `proxyrun-gui_<version>_amd64.deb` | Desktop UI; also requires the CLI package |

[Installation instructions](INSTALL.md) · [Report a bug](https://github.com/stependiant/proxyrun-releases/issues)

WSL packages run Linux applications. The UI requires WSLg.
Use the Windows installer for Windows applications.
Auto proxy may require administrator approval. If system capture stops,
applications can use ordinary system routing; there is no persistent system kill switch.

Application source is private. This repository contains downloads and documentation.
[Third-party licenses and sources](https://stependiant.github.io/proxyrun-releases/third-party/0.1.0-beta.1/proxyrun-third-party-0.1.0-beta.1.tar.gz)
are provided separately and retain their own licenses. The current beta includes
the original MIT license for Proxyrun; proprietary freeware terms have not been
applied to these installers.

Contact: rodionmasalov34@gmail.com. Do not include proxy passwords or tokens in issues.
