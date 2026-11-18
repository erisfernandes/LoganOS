<p align="center"><picture><source media="(prefers-color-scheme: dark)" srcset="marca/loganos-branco.svg"><img src="marca/loganos-preto.svg" width="96" alt="LoganOS"></picture></p>

# LoganOS

**English** · [Português](README.pt-BR.md) · [Español](README.es.md)

A home lab dashboard in a single Python file. Shortcuts to your services, a system monitor, disks with SMART health, security events, notifications, backups and small built-in apps (Notes, Links, Camera). No pip, no Docker, no database: only the Python standard library.

Named after Logan, the author's Belgian Shepherd.

## Requirements

- Linux with systemd. Tested on **Debian 13 (x86_64)**. Debian 12, Ubuntu 24.04 and Raspberry Pi OS should work but are not tested yet.
- Python 3.11 or newer (already installed on those systems).
- Root access to install.

## Install

```sh
sudo mkdir -p /opt/painel
sudo curl -fsSL -o /opt/painel/painel.py https://github.com/erisfernandes/loganos/releases/latest/download/loganos.py
sudo python3 /opt/painel/painel.py --instalar
```

Open `http://<server-ip>:8092` and create your account. The language follows your browser (English, Portuguese or Spanish) and can be changed in Settings.

## Update

From the page (Settings, Security, Versions) or in the terminal:

```sh
sudo python3 /opt/painel/painel.py --atualizar
```

The update downloads the latest release and installs it only if its SHA-256 matches the published `loganos.py.sha256`. If the new version does not start, the previous one comes back by itself.

## Uninstall

```sh
sudo python3 /opt/painel/painel.py --desinstalar
```

It asks before removing anything, and asks again before deleting your data.

## Security

- Made for your **home network and Tailscale only**. Requests from public IP addresses are refused. Do not expose it to the internet.
- On the home network the page uses plain HTTP. For HTTPS, use Tailscale (`--https`).
- The dashboard itself runs as an unprivileged systemd `DynamicUser`, not as root.
- Three small helpers run as root, each with a fixed list of actions. Nothing typed on the page becomes part of a command:
  - `painel-servicos`: reads the list of services and open ports.
  - `painel-ajudante`: reads disk health (SMART), system updates and versions.
  - `painel-pedidos`: restarts a service that has failed, mounts and unmounts USB disks, updates LoganOS and the optional password vault. The request is only a file name, checked against fixed patterns.
- No telemetry. Outbound connections, all optional or on demand: speed test (Cloudflare), new versions (GitHub), ntfy.sh as a notification fallback, a DNS check (`www.google.com`), and the pages you save in Links.

## Support

Only through [GitHub issues](https://github.com/erisfernandes/loganos/issues), with no response time. Please include the version, the system and the exported log.

## License

[AGPL-3.0](LICENSE). © 2026 Eris Fernandes.
