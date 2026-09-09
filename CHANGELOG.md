# Changelog

## 0.1.0-beta.3 - 2026-09-09

- Report a newer published version and install it on request, in the desktop and with
  `proxyrun update`. At most once a day the program reads one small static file from
  the project website and compares its version with the installed one. Skip this
  version hides one version until a newer one appears, and the whole check can be
  switched off in `Help & diagnostics`. The request carries no application
  identifier or profile data. The hosting server still sees the network address.
  A failed check shows no error and keeps any previously cached update notice.
- Update now, and `proxyrun update --install`, never run on their own. A Windows
  installation downloads the installer from this project's own release URL, requires
  the size and SHA-256 published with that release, stores it privately and runs it
  in update mode; the program then exits so its files can be replaced. A Debian
  installation requests the exact published version through its configured signed
  APT repositories and checks the installed version afterward. Source installations
  show instructions for updating manually.
- Refuse to update while desktop or CLI sessions are active, a session is starting or stopping,
  or Auto proxy is enabled. Stop the background service only when it is idle and
  block new service starts during installation.
  The Windows installer guard now waits up to 30 seconds for a self-started update to
  exit instead of refusing it immediately; it still stops nothing itself, and still
  refuses while any component keeps running.
- Keep a Windows installation's existing directory, including custom paths with
  spaces, when upgrading from installers that used the former publisher name.
  The installer migrates the directory registry entry to the English publisher
  name. Saved profiles and application settings keep their existing locations.
- Keep navigation icons and the diagnostics button inside the compact desktop
  sidebar. Profiles now use a person icon, and update actions appear together
  in a rose panel above the application list.
- Correct the CLI's system-capture guidance: authorize the launch interactively
  or pass `--change-system-routes` for that launch.

Beta 2 users must install this release through Windows Setup or APT. The built-in
updater becomes available after installing beta 3 and applies to future releases.
Update preferences use a separate file; existing profiles need no format migration.
Windows remains unsigned. The supported packages are Windows x64 and Ubuntu 24.04
amd64, including Linux applications in WSL 2. macOS remains experimental and has
no public package. System capture and Auto proxy have no persistent crash kill switch.

## 0.1.0-beta.2 - 2026-09-08

- Stopping one launch, or reaping one whose lease expired, no longer times out
  every other running launch with "session heartbeat timed out". Session teardown
  waits for the engine to exit, and on Windows for the privileged supervisor to
  acknowledge, and it no longer holds the daemon's control mutex while it waits.
- Installing the Windows capture service now verifies the capture helper against
  the digest recorded by the release build, alongside the WinDivert driver it
  already checked. The helper is copied out of a per-user directory this account
  can write, so an unverified one could otherwise have been granted a permanent
  LocalSystem service by a single administrator approval.
- The desktop reports a failure next to the profile, application or button it
  belongs to. A short label opens the full message on hover or on click, so
  nothing covers the interface and no message disappears on its own.
- The desktop opens and starts launches faster on Windows. Reading a private
  file no longer starts a PowerShell host, and the installed-application list
  and its icons are kept between runs and refreshed in the background.
- Fixed Windows command lookup choosing npm's Unix shim and failing with Win32
  error 193. PowerShell scripts now use the calling PowerShell edition and its
  execution policy, preserving script output and exit codes. Windows batch shims
  are resolved through PATHEXT when launching from cmd.
- Adopted Proxyrun Freeware License for this application release.
  Personal and commercial use of all existing features remains free. Third-party
  licenses and permissions already granted for previous MIT copies are preserved.
- Fixed duplicate native TCP streams created by retransmitted handshake packets.
- Windows in-place updates also refresh an already installed privileged capture
  helper after administrator approval.
- Updating after capture preserves an identical loaded driver. Removal can defer
  the retired driver copy until the next Windows restart, without forcing a
  restart or stopping another application's WinDivert driver.
- Auto proxy prepares and authorizes new rules before stopping working capture.
  If replacement startup fails, it attempts to restore the previous rules.
- Status distinguishes applied rules, engine failure and explicit connection
  checks, and shows the profile used for shared DNS.
- `Help & diagnostics` includes the version, guide/download links and a report
  that excludes credentials, proxy addresses and application paths.
- Desktop launches can continue in the tray. Closing explains whether Auto proxy
  continues; the tray requests attention when Auto proxy fails.
- Windows per-user Setup no longer installs a privileged service unconditionally.
  Enable the optional capture service once from Applications or the CLI.
- Windows installation/removal refuses running Proxyrun components. Use /UPDATE
  for in-place upgrades, after deliberately closing active proxy sessions.
- Ubuntu packages include an AppArmor user-namespace permission limited to the
  installed Proxyrun components.
- An older running daemon is detected without stopping its sessions.
- GLib's upstream VariantStrIter fix is backported for the Linux GUI dependency.

All existing application features remain free. The Windows installer is unsigned.
System/Auto proxy still has no persistent crash kill switch. No macOS release or
automatic in-app updater is included.

## 0.1.0-beta.1 - 2026-09-06

Initial public beta: Windows x64 Setup, Ubuntu 24.04 amd64 CLI and GUI DEBs,
saved HTTP/HTTPS/SOCKS5 profiles, default and per-app assignments, application
discovery, CLI/GUI launches, Auto proxy and an independent signed APT repository.
