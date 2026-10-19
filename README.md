# PocketBase snap

[![pocketbase](https://snapcraft.io/pocketbase/badge.svg)](https://snapcraft.io/pocketbase)

Snap packaging for [PocketBase](https://github.com/pocketbase/pocketbase), a backend with SQLite, authentication, file storage and a web dashboard.

Unofficial build, not affiliated with or endorsed by the PocketBase project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/pocketbase"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install ./pocketbase_*.snap --dangerous
sudo pocketbase superuser create admin@example.com 'your-password'
```

After publication, install from the Store with `sudo snap install pocketbase`.

The service starts right away and listens on `127.0.0.1:8090`. Open http://localhost:8090/_/ and sign in.

## Background service

```bash
sudo snap logs pocketbase       # view logs
sudo snap restart pocketbase    # restart
sudo snap stop --disable pocketbase
sudo snap start --enable pocketbase
```

### Settings

| Setting | Default | Description |
|---|---|---|
| `address` | `127.0.0.1:8090` | Address and port to listen on |

Changes restart a running service. Use `snap unset pocketbase address` to restore the default.

```bash
sudo snap get pocketbase
sudo snap set pocketbase address=0.0.0.0:8090
```

Create the administrator before opening the service to your network. For access from the internet, use a reverse proxy with HTTPS. Other settings, including SMTP, are managed in the dashboard.

## Data and backups

Data, hooks, migrations and static files are stored in `/var/snap/pocketbase/common/`, under `pb_data`, `pb_hooks`, `pb_migrations` and `pb_public`.

Dashboard backups cover `pb_data`; back up hooks, migrations and static files separately. Stop the service before copying its data. Back up before upgrading: `snap revert` does not restore data or undo migrations.

## Known limitations

- Email requires SMTP; host `sendmail` is unavailable.
- Hooks cannot freely access host files or programs.
- Updates use snapd; the upstream self-update command is removed.

## Update to a new upstream release

Change `source-tag` in `snap/snapcraft.yaml`, then rebuild. The version is taken from the tag.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). PocketBase is MIT-licensed; its dependencies carry their own licenses.
