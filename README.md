# Markhor releases

Builds of [Markhor](https://markhor.cc), a light workspace for coding agents. The source is private; this repo only
holds the macOS release files.

## Install or upgrade on a Mac

```bash
curl -fsSL https://markhor.cc/install | sh
```

It downloads the latest release, checks it against its SHA-256 checksum, and installs Markhor as a launchd agent that
starts when you log in. When it finishes it prints a link to open on your devices.

Needs macOS 13 or later (Apple silicon or Intel), the [Tailscale](https://tailscale.com) app signed in, and at least
one agent CLI on your `PATH`, such as Claude Code (`claude`), Codex (`codex`) or OpenCode (`opencode`).

Pass installer options after `sh -s --`:

```bash
curl -fsSL https://markhor.cc/install | sh -s -- --harness claude --harness codex
```

| Option | What it does |
|---|---|
| `--harness NAME` | Adds an agent. Repeat it for each one. The first is the default. |
| `--bind ADDR:PORT` | Listens here instead of your Tailscale address on port 7420. |
| `--tailscale-https` | Serves Markhor over HTTPS on your tailnet. |
| `--dry-run` | Shows what it would do. Nothing is written. |
| `--uninstall` | Stops Markhor and removes the launchd agent. Your data stays. |

## What it installs

| What | Where |
|---|---|
| The `markhor` program | `~/.local/bin/markhor` |
| The web UI | `~/.local/share/markhor/web` |
| Settings | `~/.config/markhor/markhor.env` |
| Your chats and history | `~/.markhor` |
| Logs | `~/Library/Logs/markhor` |

## Uninstall

```bash
curl -fsSL https://markhor.cc/install | sh -s -- --uninstall
```

To remove everything, also delete the folders above. Delete `~/.markhor` only if you want your history gone.
