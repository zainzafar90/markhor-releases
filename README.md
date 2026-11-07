# Markhor releases

Builds of [Markhor](https://markhor.cc), a light workspace for coding agents. The source is private; this repo only
holds the release files.

## Install or upgrade

```bash
curl -fsSL https://markhor.cc/install | sh
```

It picks the build for your OS and CPU, checks it against its SHA-256 checksum, and installs Markhor as a service that
starts on its own. When it finishes it prints a link to open on your devices.

| System | Build | Runs as |
|---|---|---|
| macOS 13 or later, Apple silicon or Intel | `markhor-macos-universal` | a launchd agent, while you are logged in |
| Linux, x86_64 or arm64 | `markhor-linux-x86_64`, `markhor-linux-aarch64` (static, any distro) | a systemd user service |
| Windows | Use the Linux build inside [WSL](https://learn.microsoft.com/windows/wsl/install) with systemd on | a systemd user service in WSL |

You also need the [Tailscale](https://tailscale.com) app signed in, and at least one agent CLI on your `PATH`, such as
Claude Code (`claude`), Codex (`codex`) or OpenCode (`opencode`). On Linux, run
`sudo loginctl enable-linger $USER` once so Markhor keeps running after you log out.

Pass installer options after `sh -s --`:

```bash
curl -fsSL https://markhor.cc/install | sh -s -- --harness claude --harness codex
```

| Option | What it does |
|---|---|
| `--harness NAME` | Adds an agent. Repeat it for each one. The first is the default. |
| `--bind ADDR:PORT` | Listens here instead of your Tailscale address on port 7420. |
| `--peer-origin ORIGIN` | Lets another Markhor (for example your laptop's) reach this one. |
| `--tailscale-https` | Serves Markhor over HTTPS on your tailnet. |
| `--dry-run` | macOS only. Shows what it would do. Nothing is written. |
| `--uninstall` | macOS only. Stops Markhor and removes the launchd agent. Your data stays. |

## What it installs

| What | Where |
|---|---|
| The `markhor` program | `~/.local/bin/markhor` |
| The web UI | `~/.local/share/markhor/web` |
| Settings | `~/.config/markhor/markhor.env` |
| Your chats and history | `~/.markhor` |
| Logs | macOS: `~/Library/Logs/markhor`. Linux: `journalctl --user -u markhor` |

## Uninstall

On macOS:

```bash
curl -fsSL https://markhor.cc/install | sh -s -- --uninstall
```

On Linux:

```bash
systemctl --user disable --now markhor.service markhor-backup.timer
```

To remove everything, also delete the folders above. Delete `~/.markhor` only if you want your history gone.
