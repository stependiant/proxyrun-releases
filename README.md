# Proxyrun — per-app proxy for Windows and Linux

Proxyrun is a **free per-application proxy client** for Windows and Linux / WSL.
Launch local coding tools such as **OpenAI Codex CLI** and **Anthropic Claude Code**,
browsers and other desktop applications with a saved **HTTP, HTTPS or SOCKS5** profile.
All current features are free: CLI, desktop UI, profiles and Auto proxy.
Bring your own proxy server; no Proxyrun account is required. Future proxy purchases
or subscriptions will be optional. Proxyrun is an independent application.

[Website and downloads](https://stependiant.github.io/proxyrun-releases/) ·
[Wiki](https://stependiant.github.io/proxyrun-releases/wiki/) ·
[Codex / Claude Code proxy guide](https://stependiant.github.io/proxyrun-releases/wiki/codex-claude-proxy/)

**0.1.0-beta.1 is available for Windows x64 and Ubuntu 24.04 amd64 / WSL 2.**
Download installers from Releases or use the signed APT repository. WinGet is not
available yet. This beta's Windows installer is unsigned.

## Use cases

| Task | How Proxyrun helps |
| --- | --- |
| Run Codex CLI or Claude Code through a proxy | Launch the installed command with a saved profile; see the guide for setup and beta validation limits. |
| Give different apps different proxies | Assign a profile to each saved application, or use a shared default. |
| Proxy apps opened from normal OS shortcuts | Enable Auto proxy for the executable and wait for the rules to apply. |
| Use the same proxy setup in a GUI and terminal | The desktop app, `prun` and `proxyrun` share profiles. |

## Codex CLI and Claude Code proxy commands

Install the coding tool separately. Create a Proxyrun profile named `work`, then
run **one** of the launch commands from your project directory:

```bash
prun configure
prun doctor --profile work
prun run --profile work codex
# Or launch Claude Code:
prun run --profile work claude
```

These commands launch local processes; they do not configure remote cloud agents.
The coding tool's normal account or API access is still required. Limited Codex
connectivity checks have passed; complete Claude Code and interactive-login
compatibility have not yet been verified for this beta.
[Read the setup and troubleshooting guide](AI-TOOLS.md).

## How to use Proxyrun

1. Install Proxyrun and open **Profiles**.
2. Add your proxy server address, port, protocol and optional credentials.
3. Save it and click **Check connection**.
4. Open **Applications**, choose an app and click **Launch**.

Use the pencil button on an application to choose its **Proxy profile**.
**Use default profile** follows the star-marked profile in Profiles.
Enable **Auto proxy** if you want the application to use the proxy when opened
from its usual OS shortcut; wait for the rules to apply and restart the app.

Prefer the terminal? Create a profile with `prun configure`, then launch an
installed app with `prun chrome` or `prun run --profile work chrome`.
`prun` and `proxyrun` share settings with the desktop app.

[Read the Wiki](https://stependiant.github.io/proxyrun-releases/wiki/) ·
[User guide on GitHub](USER-GUIDE.md) ·
[Report a bug](https://github.com/stependiant/proxyrun-releases/issues/new)

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
