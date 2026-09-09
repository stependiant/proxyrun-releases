# Privacy

Proxyrun stores proxy profiles and application assignments on your device. Proxy
passwords are stored in files restricted to the user account; they are not
protected against an administrator or malware running as that user. Protect your
OS account and backups. Editing a profile does not send its saved password back
to the desktop form.

No Proxyrun account, analytics or telemetry service is required. Application
traffic goes to the proxy you configure. That provider and destination services
have their own policies. HTTPS traffic retains its destination TLS connection;
Proxyrun's connection check verifies certificates.

Check connection makes an explicit HTTPS request to example.com through the
selected proxy. Shared DNS in Auto proxy uses one of the assigned profiles, shown
in the interface. A proxy hostname may first be resolved by the operating system.

Local session diagnostics can show connection destinations and traffic counters;
private recovery snapshots can contain network configuration. Do not publish
those files or raw configuration directories. `Help & diagnostics` and the
`proxyrun diagnostics` command use a separate allowlist that excludes credentials,
proxy addresses, profile names, executable paths and connection history. Nothing
is uploaded automatically. Review any report before choosing to share it.

Proxyrun tells you when a newer version is published. At most once a day it
downloads one small file from the project website and compares the version in it
with the installed one. The request contains no application identifier, account,
profile or installation age. Every user requests the same file. The hosting
server sees your network address, and the request uses your environment's proxy
settings. Switch the check off in `Help & diagnostics` to disable these requests.
The CLI checks only when you run `proxyrun update`; it uses the same preference
and daily cache as the desktop.

Nothing installs itself. Update now, and `proxyrun update --install`, act only
when you choose them. On Windows that downloads the published installer from the
project's own releases, checks it against the checksum published with the release
and runs it. On Ubuntu it upgrades through the signed APT repository you
configured, so APT's own signature check applies and your system records the
change as usual. Both refuse while sessions are active, starting or stopping, or Auto proxy
is enabled. Only an idle background service is stopped. Neither sends anything
about your configuration.

Opening the user guide or downloads page uses your browser and contacts GitHub.
The public download site is hosted on GitHub Pages. Optional future proxy sales
or subscriptions are not part of this version and will need their own terms.
