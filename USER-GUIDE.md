# Proxyrun Wiki

Windows x64 and Ubuntu 24.04 / WSL 2 · 0.1.0-beta.3.

## Contents

- [Quick start](#quick-start)
- [Installation](#installation)
- [Create a proxy profile](#profiles)
- [Check connection and latency](#check-connection)
- [Launch applications](#applications)
- [Auto proxy for normal OS launches](#auto-proxy)
- [Interactive terminal applications](#interactive-terminal)
- [Command-line quick reference](#command-line)
- [Troubleshooting](#troubleshooting)
- [Updates and removal](#updates-and-removal)
- [Diagnostics, background use and updates](#diagnostics-updates)

<a id="quick-start"></a>

## Quick start

Proxyrun runs applications through a proxy you provide. It does not include a proxy server or a proxy subscription. All current desktop and CLI features are free; no Proxyrun account is required.

1. Install Proxyrun for your operating system.
2. Open Profiles and add the server details supplied by your proxy provider.
3. Save the profile, then click Check connection.
4. Open Applications, find your app and click Launch.

A profile is a saved proxy connection: its address, port, protocol and optional credentials. Each app can use a specific profile or follow your default. The animated network on the homepage is an illustration; changing it does not configure the installed application.


<a id="installation"></a>

## Installation

### Windows x64

1. Download Proxyrun-Windows-x64-Setup.exe from the release page.
2. Run Setup for your user account. Enable the optional capture service in Applications when you want to avoid an administrator prompt for each ordinary launch. Windows asks for approval when you enable it.
3. Open Proxyrun from the Start menu. Open a new terminal if you want to use prun or proxyrun commands.

The installer includes the desktop UI and CLI. This beta is unsigned, so Windows may show a publisher or SmartScreen warning. Check that you downloaded it from the official release page; the website provides SHA256 checksums.

### Ubuntu 24.04 amd64 and WSL 2

Use the signed APT repository setup in the installation guide. Once that repository is configured, install the desktop UI and CLI together:

```bash
sudo apt update
sudo apt install proxyrun-gui
```

For CLI only, install proxyrun instead. For manual installation, download both DEB files into the same folder and run:

```bash
sudo apt install ./proxyrun_0.1.0-beta.3_amd64.deb ./proxyrun-gui_0.1.0-beta.3_amd64.deb
```

WSL packages run Linux applications. To proxy a Windows application, use native Windows Proxyrun. The Linux desktop UI under WSL requires WSLg. These packages target Ubuntu 24.04 amd64; other distributions and macOS are not part of this release. WinGet submission is pending.

[Full installation and APT setup](https://github.com/stependiant/proxyrun-releases/blob/main/INSTALL.md)

[Download the beta installers](https://github.com/stependiant/proxyrun-releases/releases/tag/v0.1.0-beta.3)


<a id="profiles"></a>

## Create a proxy profile

Open Profiles and add a new profile. Copy the connection details from your proxy provider; do not enter the address of the website you want to visit.

| Field | What to enter |
| --- | --- |
| Profile name | A name such as work or proxy-1. Use English letters, digits, hyphens or underscores. |
| Proxy type | HTTP · CONNECT, HTTPS · TLS to proxy, or SOCKS5, as specified by the provider. |
| Server address | The proxy hostname or IP address, such as proxy.example.com. |
| Port | The proxy port, such as 8080 or 1080. |
| Username / Password | The provider's credentials. Leave them blank if authentication is not required. |

HTTP proxies can open HTTPS websites using CONNECT. Choose HTTPS only when the connection to the proxy server itself uses TLS; the type is not determined by the website URL. Enable SOCKS5 UDP only if the provider supports UDP forwarding.

Save the profile and check its connection. The first profile becomes the default. Use the star button on another profile to set it as default. Applications with Use default profile follow that selection; applications with a specific profile keep their own choice.

Editing a profile keeps its saved password unless you enable Change password. Deleting a profile assigned to an app requires selecting a replacement before launching that app. Changing the default does not move an already running ordinary launch to another proxy; stop and relaunch it.


<a id="check-connection"></a>

## Check connection and latency

Click Check connection on a saved profile. Proxyrun makes an HTTPS request to example.com through that proxy and verifies the TLS certificate. A successful check shows the measured response time in milliseconds.

This number includes connection and TLS setup. It is an HTTPS response measurement, not ICMP ping. A successful check confirms that request; it does not guarantee access to every destination, UDP support or compatibility with every app.

1. If the check fails, verify the proxy protocol, server address and port.
2. Check the username/password and whether the provider requires your IP address to be allowed.
3. Confirm that the proxy service is active and permits the destination.
4. Read the error before changing other settings; changing HTTP to HTTPS does not automatically fix a connection failure.


<a id="applications"></a>

## Launch applications

1. Open Applications. Proxyrun discovers supported installed applications automatically.
2. Search for an app, or refresh the list after installing new software.
3. Use the pencil button to choose its Proxy profile. Leave Use default profile selected if it should follow your default.
4. Save the application and click Launch. Wait for its running state.
5. Click Stop to end that Proxyrun-owned launch.

### Add a missing application

Click Add application. Enter a display name and use the folder button beside Path to app to select the executable. A supported command such as chrome can also be used. A Windows Chrome path is commonly:

```text
C:\Program Files\Google\Chrome\Application\chrome.exe
```

Paths depend on where you installed the program. Use the actual executable, not a website URL. Store aliases, Flatpak/Snap launchers and applications needing special launch wrappers may require additional configuration and are not guaranteed to work just because they appear in a system menu.

Launch arguments accepts one argument per line. Spaces within a line are preserved; do not paste a full shell command there. Deleting an application entry removes it from Proxyrun's list, not from your computer.

### Browsers and existing windows

An ordinary Launch manages the new application instance. It does not automatically take over every window that was already open. Chromium-based browser launches use a separate browser data directory, so Chrome may open without your usual signed-in profile or extensions.


<a id="auto-proxy"></a>

## Auto proxy for normal OS launches

Use Auto proxy when you want to open an application from its usual Start menu, desktop shortcut or launcher and have its connections use the selected proxy.

1. In Applications, edit the application with the pencil button.
2. Enable Auto proxy and choose a Proxy profile, or Use default profile.
3. Save the settings and approve system authorization if requested.
4. Wait until Proxyrun has applied the rules. If it reports an error, address it and use Retry.
5. Close and restart an already running application, then open it from its normal OS shortcut.

Apps with Auto proxy enabled appear above the other applications. Rules use executable paths and apply to all instances of those applications. You can assign different proxies to different apps. Separate helper executables may need their own entries.

Auto proxy continues when the GUI is closed and is configured to restart at sign-in. Linux graphical autostart requires a supporting desktop session; headless WSL is not a graphical login session. Windows may request administrator approval when system capture starts or its configuration changes.

To turn it off for an app, edit the app and clear Auto proxy. Disabling all rules stops Auto proxy capture. An invalid edit can leave the previous rules active; check the status message rather than assuming the new selection was applied.

### Understand the difference from Launch

Auto proxy changes system routes and DNS while active. It is not a persistent firewall kill switch: startup failure or a capture-engine crash can leave normally launched apps using ordinary system routing. Do not assume a failed or stopped Auto proxy session blocks all direct traffic. With several profiles, application connections follow their assignments, but intercepted DNS is shared and uses the first profile in name order.

Beta 2 checks and authorizes new settings before stopping working rules. If the new engine fails to start, it attempts to restore the previous rules. This is not an atomic switch: direct connections may be possible during replacement. Rules active means the engine is running, not that a proxy connection has been checked. The interface shows which profile carries shared DNS.


<a id="interactive-terminal"></a>

## Interactive terminal applications

For an interactive command, add the command or its executable in Applications, enable Open in terminal and choose its proxy profile. The command must already be installed and runnable on that operating system.

On Windows, prun launched from PowerShell uses that edition's external-command lookup and runs .ps1 scripts with its inherited execution policy. Script errors and exit codes come from PowerShell itself. An npm command with .ps1, .cmd and Unix wrappers uses the appropriate Windows wrapper; explicit .cmd and .bat commands are also supported. PowerShell profiles are not run again, and interactive functions and aliases are not copied into the child process.

Launch opens an interactive terminal window for keyboard input. Closing that terminal window keeps its process running; reopen it from the application row. Use Stop when you want to end the launch.

The main window asks before closing when it owns running application launches. You can keep launches running in the tray. Closing an idle GUI does not stop CLI-owned sessions or saved Auto proxy rules.


<a id="command-line"></a>

## Command-line quick reference

prun and proxyrun are two names for the same CLI. They share profiles and the default selection with the desktop UI. You do not need to start a separate service terminal for an ordinary launch.

### Create and check a profile

```bash
prun configure
prun profiles
prun doctor --profile work
```

The configure wizard asks for a name, type, address, port and optional credentials. Password input is hidden. In the example above, replace work with the name you created.

### Choose the default and launch

```bash
prun profile default
prun profile default work
prun chrome
prun codex
prun run --profile work chrome
```

The applications must be installed. Put Proxyrun options before the program name; arguments after the program name are passed to that program. The explicit --profile option affects that launch.

### Inspect or stop sessions

```bash
prun status
prun connections SESSION_ID
prun stop SESSION_ID
prun --help
prun run --help
```

Replace SESSION_ID with an ID from status. prun shutdown stops the shared background service and its sessions; use it only when you intend to stop those proxy sessions. On Windows, prun service status reports the installed capture service.


<a id="troubleshooting"></a>

## Troubleshooting

### An app is missing from Applications

Refresh the application list, then use Add application and browse to its executable. Confirm you are using Windows Proxyrun for a Windows app, or Linux Proxyrun for a Linux app.

### Check connection works, but an app fails

Check the app's assigned profile, its path and the error shown for the launch. The connection check tests one HTTPS destination. Apps may use different destinations, UDP, helper processes or existing instances. HTTP-only profiles do not provide general UDP forwarding; SOCKS5 UDP requires provider support.

### The app closes with a native proxy transport error

Some capture failures stop the Proxyrun-owned application instance to avoid releasing that instance's traffic directly. Check the profile connection, then collect the exact launch error and reproduction steps. This behavior is not a system-wide guarantee for Auto proxy or other running apps.

### Auto proxy does not apply or asks for administrator rights

Wait for rules to become ready, approve the required system authorization and restart the target app. Use Retry after resolving the reported issue. The service installed on Windows handles ordinary instance launches; Auto proxy uses system capture and can still ask for authorization.

### prun is not found

On Windows, open a new terminal after Setup updates PATH. On Linux, confirm the proxyrun package is installed. The proxyrun-gui package installs it as a dependency.

### The Linux UI does not open in WSL

Use Ubuntu 24.04 amd64 on WSL 2 with working WSLg for the GUI. In a headless environment, use the CLI. WSL packages cannot proxy native Windows programs as Linux application instances.

[Report a bug](https://github.com/stependiant/proxyrun-releases/issues/new)

Include your Proxyrun version, OS, exact error and the smallest set of steps that reproduces the problem. Issues are public: remove proxy credentials, tokens, packet captures and working exploits before posting.


<a id="updates-and-removal"></a>

## Updates and removal

Beta 2 has no built-in updater. Install beta 3 through Windows Setup with /UPDATE or your configured APT repository. Saved profiles need no format migration. Windows Setup preserves your existing installation directory, including custom paths with spaces.

After installing beta 3, Proxyrun can report future releases. It reads one small file from the project website at most once a day. Update now asks for confirmation before installing. Skip this version hides that release until a newer one appears. Turn off Tell me when a new version is published in Help & diagnostics to disable the check.

On Windows, Update now downloads the published installer, verifies its size and SHA256, then starts it. Proxyrun closes so Setup can replace its files. On Ubuntu, the package manager requests the exact version from your configured signed APT repositories and asks for system authorization. Reopen Proxyrun after installation to use the new build. Source installations show instructions for updating manually.

Finish desktop and CLI sessions and disable Auto proxy before updating. The updater refuses active sessions and unfinished starts or stops. It stops only an idle background service. In a terminal, use proxyrun update to check, proxyrun update --install to install, or proxyrun update --skip to hide the offered version.

Before running Windows Setup manually or removing Proxyrun, close active launches and the GUI, disable Auto proxy and run proxyrun shutdown when you are ready to stop the remaining proxy sessions. Other programs may depend on those sessions. Run the new official Setup with /UPDATE for an in-place update. To uninstall, use Windows Settings, then Apps after the background components have stopped. If upgrading from the earlier ZIP preview, uninstall that preview with install.cmd -Uninstall before using Setup. Saved profiles are preserved. If Windows still holds the loaded capture driver during removal, Proxyrun schedules only its retired driver copy for deletion at the next restart. The uninstaller reports that a restart is needed; it never restarts Windows automatically. Reinstalling before that restart does not put the new files on the deletion list.

On Ubuntu or WSL with the APT repository configured, update using:

```bash
sudo apt update
sudo apt upgrade
```

Before removal, close the GUI and apps using its proxy sessions. Then stop Proxyrun as your normal user and remove the packages:

```bash
prun shutdown
sudo apt remove proxyrun-gui proxyrun
```

Removing the packages preserves saved profiles. Keep proxy credentials private when backing up configuration or sharing screenshots.


<a id="diagnostics-updates"></a>

## Diagnostics, background use and updates

Open Help & diagnostics to see the installed version, review a report and save it. The CLI equivalent is proxyrun diagnostics. It reports versions and component status without credentials, proxy addresses, profile names, application paths or connection history. It does not start capture or test an external connection. Review the report before sharing it.

When closing with active desktop launches or Auto proxy enabled, choose Keep in background to hide the window in the system tray. Reopen it from the tray or launch Proxyrun again. Exit desktop stops desktop-owned launches; Auto proxy and independent CLI sessions continue. Disable Auto proxy explicitly to stop its rules.

Manual updates use Windows Setup with /UPDATE or the configured APT repository. Windows Setup requests administrator approval to refresh an installed capture service. It waits up to 30 seconds for running components to exit and refuses the update if they remain active. It never closes them forcibly. If Proxyrun reports an older running background component, finish its sessions and restart it deliberately.
