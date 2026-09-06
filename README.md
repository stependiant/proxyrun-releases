# Proxyrun

Run applications through your own HTTP, HTTPS or SOCKS5 proxy.
All current features are free: CLI, desktop UI, profiles and Auto proxy.
No account is required. Future proxy purchases or subscriptions will be optional.

The first beta is in preparation. WinGet and APT are not available yet.

## Download

Choose from the three installers in [Releases](https://github.com/stependiant/proxyrun-releases/releases):

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
will be available when the release is published; they retain their own licenses.

Contact: rodionmasalov34@gmail.com. Do not include proxy passwords or tokens in issues.
