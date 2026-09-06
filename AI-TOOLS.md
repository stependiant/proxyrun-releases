# Codex and Claude Code through a proxy

Launch an installed AI coding tool with your own proxy profile. Proxyrun provides a free desktop UI and CLI for Windows x64 and Ubuntu 24.04 amd64, including Linux applications in WSL 2.

## Contents

- [What Proxyrun does](#what-proxyrun-does)
- [Install and save a proxy profile](#prepare-a-profile)
- [Launch Codex CLI through a proxy](#codex-cli-proxy)
- [Launch Claude Code through a proxy](#claude-code-proxy)
- [Launch from the desktop UI](#desktop-launch)
- [Windows, Linux and WSL](#windows-linux-wsl)
- [Check a failing connection](#connection-troubleshooting)

<a id="what-proxyrun-does"></a>

## What Proxyrun does

Proxyrun is a per-application proxy client: you save a proxy server as a profile and choose that profile when launching a program. Profiles support HTTP CONNECT, HTTPS to the proxy server and SOCKS5. The same profiles are available in the desktop UI and the terminal.

This guide covers local Codex CLI and Claude Code processes. Proxyrun does not provide AI models, an API gateway, a proxy subscription or access to an AI account. It does not change networking inside a remote coding agent's cloud environment. Install the coding tool separately and keep its normal account or API setup.

The instructions use Proxyrun's general application launcher. Limited real Codex CLI connectivity checks have passed; full interactive, fresh-login and Claude Code compatibility checks have not been recorded for this beta. Validate the workflow you need with your proxy provider.


<a id="prepare-a-profile"></a>

## Install and save a proxy profile

1. Install Proxyrun. On Ubuntu or WSL, first connect the Proxyrun APT repository using the installation guide; a stock Ubuntu installation cannot find the package yet.
2. Install Codex CLI or Claude Code in the same operating system where you run Proxyrun. Confirm that codex or claude is available in that terminal.
3. Run prun configure and create a profile named work. Enter your proxy provider's address, port, protocol and optional credentials.
4. Check the profile with prun doctor --profile work, or use Check connection in the desktop Profiles tab.

```bash
prun configure
prun doctor --profile work
```

Replace work in the examples with your saved profile name. The connection check makes one HTTPS request through the proxy; a successful result does not prove that the AI provider or every helper process is reachable.

[Install Proxyrun on Windows or Ubuntu / WSL](https://github.com/stependiant/proxyrun-releases/blob/main/INSTALL.md)


<a id="codex-cli-proxy"></a>

## Launch Codex CLI through a proxy

From your project directory, use the explicit run command to launch the installed codex executable with the work proxy profile:

```bash
prun run --profile work codex
```

For repeated launches, set the default profile once and use the shorter command:

```bash
prun profile default work
prun codex
```

This starts a new local Codex CLI process. It does not reconfigure a Codex session that is already running, a browser login window opened separately or a cloud task. Keep any existing working proxy wrapper in place until you have verified a separate Proxyrun launch.

[Official Codex CLI documentation](https://developers.openai.com/codex/cli/)


<a id="claude-code-proxy"></a>

## Launch Claude Code through a proxy

Use claude as the application command after installing Claude Code. This targets Claude Code in your terminal, not the Claude website or a separate desktop application:

```bash
prun run --profile work claude
```

If you already selected a default Proxyrun profile, the equivalent short launch is:

```bash
prun claude
```

Claude Code also documents its own HTTP_PROXY and HTTPS_PROXY settings. Existing tool-level proxy settings can affect the route inside a Proxyrun launch. Keep track of which configuration you are testing; avoid stacking proxy settings without understanding the resulting route. Proxyrun supports SOCKS5 profiles, but that does not mean a SOCKS URL is accepted by every coding tool's own HTTPS_PROXY setting.

[Official Claude Code network configuration](https://code.claude.com/docs/en/corporate-proxy)


<a id="desktop-launch"></a>

## Launch from the desktop UI

1. Open Applications → Add application.
2. Use Codex or Claude Code as the display name.
3. In Path to app, select the installed executable or enter the installed command, codex or claude.
4. Enable Open in terminal so the coding tool can receive keyboard input.
5. Choose the Proxy profile, save the entry and click Launch.

Choosing a profile in an application's UI settings applies to that saved application entry. For CLI launches, use --profile explicitly or set the shared default profile. The CLI examples do not look up an application row's pinned profile by its display name.

For launches from ordinary OS shortcuts, consider Auto proxy in the application's settings. Its executable-path rules differ from a Proxyrun-owned Launch and can require system authorization. Shared runtimes such as node.exe can also be used by unrelated applications, so review the executable you are assigning.

[Auto proxy behavior and limitations](https://stependiant.github.io/proxyrun-releases/wiki/#auto-proxy)


<a id="windows-linux-wsl"></a>

## Windows, Linux and WSL

| Where the tool runs | Which Proxyrun to use |
| --- | --- |
| Windows executable | Use Windows Proxyrun from PowerShell or the desktop UI. |
| Ubuntu 24.04 amd64 | Use the Linux CLI package or desktop UI. |
| Linux executable inside WSL 2 | Install Proxyrun and the coding tool inside that WSL distribution. WSLg is needed only for the GUI. |

An executable under a mounted Windows directory is not automatically a Linux program. Linux Proxyrun rejects Windows PE executables in WSL because its Linux network isolation does not cover them. If a package-manager shim or shell alias cannot be launched, select the real executable; for a JavaScript entry point, select the Node executable and pass the script path as a launch argument.

This release targets Windows x64 and Ubuntu 24.04 amd64 / WSL 2. There is no macOS download in this beta.


<a id="connection-troubleshooting"></a>

## Check a failing connection

1. Check the selected profile and its credentials. HTTP CONNECT can carry HTTPS requests; select HTTPS as the proxy type only when the proxy endpoint itself uses TLS.
2. Check that the coding tool is installed and visible in the same OS and terminal where you run prun.
3. Read the launch error and inspect active sessions with prun status. Use prun connections SESSION_ID with the session ID shown there.
4. Check the AI provider's authentication and the destinations your proxy permits. Proxyrun does not replace the provider's account requirements.
5. If a separately opened browser, container, sandbox or helper process is involved, verify its route separately. Do not treat one successful request as proof that all application traffic is covered.

```bash
prun status
prun connections SESSION_ID
```

Auto proxy does not provide a persistent system kill switch. Normally launched applications can use ordinary system routing after capture stops or fails. See the main Wiki before relying on Auto proxy for a sensitive workflow.

[Read the complete Proxyrun Wiki](https://stependiant.github.io/proxyrun-releases/wiki/)

[Report a bug without credentials or tokens](https://github.com/stependiant/proxyrun-releases/issues/new)
