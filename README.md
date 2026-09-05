# Proxyrun

Free desktop and command-line application for running applications through your
own HTTP, HTTPS or SOCKS5 proxy. Profiles, per-application proxy selection and
Auto proxy are free. No account is required for your own proxies.

This repository contains official downloads, documentation and issue tracking.
It does not contain the proprietary application source. Third-party components
retain their licenses and corresponding-source distribution information.

The first beta is being prepared for Windows x64 and Ubuntu 24.04 amd64, including
Ubuntu 24.04 under WSL 2. Packages are not available through WinGet or APT yet.
Only download versions marked as published releases; availability is announced
here after package validation.

On Windows the installer includes both CLI (`proxyrun` / `prun`) and GUI. It
prepares the capture service with Windows administrator authorization.
On Linux `proxyrun-gui` depends on `proxyrun`; install `proxyrun` alone for CLI use.
WSL GUI needs WSLg. Linux/WSL capture targets Linux applications; Windows
applications need the Windows version.

Auto proxy can change system routes and DNS, can require administrator approval,
and has no persistent system kill switch. If system capture stops, applications
can use ordinary system routing. Proxy compatibility depends on the provider.

Future in-app proxy purchases or subscriptions will be optional; existing local
features and manual use of your own proxy remain free.

Report ordinary bugs in Issues after removing passwords, tokens and proxy URLs
with credentials. Report sensitive vulnerabilities privately to
rodionmasalov34@gmail.com.
