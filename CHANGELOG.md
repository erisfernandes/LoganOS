# Changelog

## 1.83.0 (2026-11-25)

Brings everything since 1.69.1 in a single update.

- New **Tasks** system app: lists, groups, steps, due dates, My Day, starred and archived lists, trash, swipe gestures on phones and pull to refresh. It can be added to the iPhone home screen as its own app. Optional terminal access with `--tarefas`, or over SSH with a key restricted to that command (`--tarefas-ssh`).
- **Backup**: prepare a USB stick as the backup destination from the page (password required); **folder copy**, which copies chosen folders (photos, documents) to another disk after each backup with rsync, into `loganos-copias` on that disk. Nothing is ever deleted from the copy, and only folders under `/mnt` or `/media` on a disk other than the system disk and the destination are accepted.
- **Settings, Terminal commands**: Debian shortcuts and commands by topic, each with what it does, a search box and a copy button. Only in Portuguese for now; the translation will come in a later version.
- Read-only display key and `/api/visor` endpoint for small status screens.
- Optional switch to delete unused Docker images (in Security, Versions; off by default).
- System apps show an icon per app, with icon buttons for export, import and uninstall.
- The Vault backup option appears when the Vaultwarden folder is readable only by root.
- Layout fixes on phones and in Settings.

## 1.69.1 (2026-11-18)

- Fix: on machines with the LoganOS backup configured, the 1.69.0 migration started the dashboard with an empty data folder (the data stayed untouched in the old folder). Running `--instalar` of 1.69.1 moves the data and fixes it. The backup state now lives in `/var/lib/loganos-backup`.

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
