# Fablerift releases

This repository holds the downloadable builds of **Fablerift**, a multiplayer text adventure (MUD). There is no
source code here — it is the download page, and it is also what the software reads: the launcher checks the
[latest release](https://github.com/SleepyE5/Fablerift-releases/releases/latest) for updates, and
`official-servers.json` is the server list the desktop app offers to join.

Want to play without installing anything? The official server runs in the browser at
**[play.fablerift.net](https://play.fablerift.net)** — the same world, no download.

## Download

Open the [latest release](https://github.com/SleepyE5/Fablerift-releases/releases/latest) and pick your platform:

| Your computer | Bundle | Install it |
|---|---|---|
| Windows 10 or 11, 64-bit | `Fablerift-launcher-win-x64.zip` | Unzip, run `install-windows.ps1` (`uninstall-windows.ps1` is beside it). |
| Linux, x86_64 | `Fablerift-launcher-linux-x64.zip` | Unzip, run `./install-linux.sh` (`uninstall-linux.sh` is beside it). |
| macOS with Apple Silicon | `Fablerift-launcher-osx-arm64.zip` | Unzip, run `./install-macos.sh` (`uninstall-macos.sh` is beside it). |

Each script installs into your own account's files and puts the launcher in your Start Menu or applications menu. No
administrator password, and no ARM64 Windows, ARM64 Linux, Intel Mac or 32-bit builds are published.

### One-click installers

Two single-file installers are published as well, on the
[v1.3.4](https://github.com/SleepyE5/Fablerift-releases/releases/tag/v1.3.4) release — the newest build of either
installer, because the two packages are not rebuilt for every version:

| Your computer | Installer |
|---|---|
| Windows 10 or 11, 64-bit | `Fablerift-1.3.4-win-x64.msi` — installs with no elevation: it puts the game in `%LOCALAPPDATA%\Fablerift`, so it belongs to the account that plays it. One quirk of Windows Installer on a shared PC: the *Add or remove programs* line is listed for every account even though the game and its removal belong to one, and uninstalling from an account that never installed it just tells you it isn't installed there. |
| Linux, x86_64 | `Fablerift-1.3.4-x86_64.AppImage` — one file: `chmod +x` it and run it. No root and no package manager. |

Each has a `.sha256` file beside it. **An installer is only worth downloading once** — the launcher it puts on your
machine keeps itself current from then on, so a 1.3.4 install becomes a 1.3.5 install the first time it starts and
checks. If you already have Fablerift, you do not need to reinstall for a newer version. Older installer packages stay
attached to their own release tags if you need a specific one.

## Updates

The launcher checks this repository when it starts. When a newer release is here it asks before downloading and
installing it, and keeps the two previous installs beside the new one so a bad update can be rolled back.

## Check what you downloaded

The main archive of every release, the hosting kit and both installers have a `.sha256` file beside them. From the
folder you downloaded to:

```sh
sha256sum  -c Fablerift-v<version>-release.zip.sha256      # Linux
shasum -a 256 -c Fablerift-v<version>-release.zip.sha256   # macOS
```

It prints `OK` for each file the checksum covers. `Fablerift-v<version>-release.zip` is everything in one archive —
all three launcher bundles, the server builds, the hosting kit and the checksums.

## Run your own server

The same release carries the hosting kit, for anyone who wants their own world rather than the official one:

| File | What it is |
|---|---|
| `Fablerift-hosting-linux-x64.tar.gz` | The Linux server, the deployment scripts and the game data. |
| `install-official-server.sh` | Run it as root on a Debian or Ubuntu machine and it installs or updates everything: the game under its own locked-down account, systemd units, a health check, a backup before every update, automatic rollback, a daily re-run that keeps it current and a backup every 15 minutes. It publishes through Tailscale Funnel by default, or a Cloudflare Tunnel if you bring a token; telnet and the admin panel stay off until you ask for them. Running it again updates in place. |
| `proxmox-create-official-server.sh` | Creates the container on a Proxmox host first — an unprivileged Debian 12 LXC, 2 cores, 2 GB RAM and 8 GB disk by default — then runs the installer inside it. |
| `official-servers.json` | The server list the desktop app offers to join. |

`docs/ops/official-server.md` in the game's source repository explains the settings each script takes.

## Play with a MUD client

Telnet players and Mudlet reach the official server at **`mud.fablerift.net`**: port **4000** unencrypted, port
**4443** with *Secure* ticked. Mudlet can install the Fablerift package straight from the game at
`https://play.fablerift.net/mudlet/Fablerift.mpackage` — it adds the buttons, the map panel and the command
shortcuts, and the game pushes its map and status to Mudlet over GMCP and MSSP.

## Questions

**EnricoFJS@gmail.com** — server owners and players alike.
