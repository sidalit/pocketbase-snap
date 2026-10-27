<div align="center">

<img src="snap/gui/pocketbase.png" alt="PocketBase logo" width="128" />

# PocketBase

**A realtime backend in one application.**

[![pocketbase](https://snapcraft.io/pocketbase/badge.svg)](https://snapcraft.io/pocketbase)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [PocketBase](https://ganigeorgiev.com/pocketbase/pocketbase), a backend with a database, authentication, file storage and an admin dashboard.

</div>

---

## Getting Started

<a href="https://snapcraft.io/pocketbase"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install pocketbase
sudo pocketbase superuser create admin@example.com 'your-strong-password'
```

Use your own email and password, then open [http://127.0.0.1:8090/_/](http://127.0.0.1:8090/_/). The service starts automatically. Create the superuser before exposing it to your network.

## Configure

| Setting | Accepted values | Default |
| --- | --- | --- |
| `address` | `host:port` or `[IPv6]:port`; port `1`–`65535` | `127.0.0.1:8090` |

```bash
sudo snap get pocketbase
sudo snap set pocketbase address=0.0.0.0:8090
```

Changes restart the running service. `sudo snap unset pocketbase address` restores the default. Use an HTTPS reverse proxy for internet access. Configure SMTP and other application settings in the dashboard.

Data lives under `/var/snap/pocketbase/common`:

| Directory | Contents |
| --- | --- |
| `pb_data` | Database and uploaded files |
| `pb_hooks` | JavaScript hooks |
| `pb_migrations` | Database migrations |
| `pb_public` | Static website files |

Dashboard backups cover `pb_data` only. Back up the other directories separately; stop the service before copying its data manually.

## Limitations

- Email requires SMTP; host `sendmail` is unavailable.
- Hooks can only access files and programs allowed by strict confinement.
- Updates come through snapd. Back up before upgrading: `snap revert` does not undo database migrations or restore shared data.

## Build

```bash
git clone https://github.com/sidalit/pocketbase-snap.git
cd pocketbase-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/pocketbase-snap/issues).
- **Application bugs:** [report them upstream](https://ganigeorgiev.com/pocketbase/discussions?category=Bugs).

## License

Snap packaging: [MIT](https://github.com/sidalit/pocketbase-snap/blob/main/LICENSE).
