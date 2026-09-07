# Changes

## 0.1.0-beta.2 — 2026-09-08

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
- Help & diagnostics includes the version, guide/download links and a report
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

## 0.1.0-beta.1

Initial public beta: Windows x64 Setup, Ubuntu 24.04 amd64 CLI and GUI DEBs,
saved HTTP/HTTPS/SOCKS5 profiles, default and per-app assignments, application
discovery, CLI/GUI launches, Auto proxy and an independent signed APT repository.
