# Security reports

For a suspected vulnerability, email **rodionmasalov34@gmail.com** privately.
Include the version, operating system and a minimal reproduction without real
proxy credentials. Do not post exploit details, private profiles, tokens or
packet captures in a public issue. GitHub's private reporting button can be used
if the repository owner has enabled it; email remains the fallback.

For ordinary bugs, use [public issues](https://github.com/stependiant/proxyrun-releases/issues/new).
Include expected/actual behavior and a reviewed report from Help & diagnostics
or `proxyrun diagnostics`. Reports and issues are not uploaded automatically.

The optional Windows capture service runs as LocalSystem. Before installing it,
Proxyrun verifies the driver and the capture helper against the digests recorded
by the release build and installs exactly the bytes it checked. Beta packages are
unsigned, so enable the service only from a package you trust, on a machine you
believe is not already compromised. Launches without the service authorize each
one separately and leave nothing installed.

The beta has not had an independent security audit. Auto proxy and system capture
do not provide a persistent firewall kill switch. A crash or rule replacement
can permit direct connections; see the user guide for platform limitations.
