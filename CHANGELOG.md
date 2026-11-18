# Changelog

## 1.69.0 (2026-11-18)

- Everything LoganOS creates on the system is now named `loganos`: `loganos.service`, the `loganos-*` helpers and the data folder `/var/lib/private/loganos`. Installations from earlier versions are migrated by `--instalar`, keeping the account, the data and the port.
- Recommended location is now `/opt/loganos/loganos.py`. Any folder outside `/root`, `/home` and `/tmp` works.
- Fix: `--desinstalar` stopped early on machines without Tailscale.
- Downloaded files are named `loganos-*`.

## 1.68.2 (2026-11-18)

- Fix: the Links app could not read the title and icon of a pasted page since 1.66.0.

## 1.68.1 (2026-11-18)

- Releases are signed with minisign (key 407236916ABFC1EF). From this version on, updates are installed only when the signature matches. Verify by hand with `minisign -Vm loganos.py -P RWTvwb9qkTZyQBKWsZ2B8t/Fbq7kBgZ9Feuvr66yYaP0Y6aqZhf9XcG6`.
- Decimal values from the server (like backup sizes) follow the page language.
- Missing translation of "Method not allowed".

## 1.67.0 (2026-11-18)

First public release.

- Requests from public IP addresses are refused; the dashboard is for the home network and Tailscale.
- Updates from the latest GitHub release, installed only when the published SHA-256 matches.
- `--desinstalar` removes LoganOS and, after a second confirmation, its data.
- `--instalar` asks for the port on a new machine.
- Notifications are sent in the language chosen on the page.
- Podman is used when Docker is not installed.
- Missing English and Spanish translations of the page completed.
- Logo on the sign-in page and an About section with the author and license.

Versions before 1.67.0 were developed privately.
