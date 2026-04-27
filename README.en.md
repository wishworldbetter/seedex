# Seedex

**English** · [日本語](./README.ja.md) · [简体中文](./README.md)

**The iPhone remote control for Claude Code.** Scan once to pair, and your iPhone instantly mirrors every Claude Code session on your Mac — with the ability to start or take over conversations in real time. A complete replacement for the official Claude Code remote workflow, with all data staying on your own Mac.

## Features

- **No sign-in** — One QR scan and you're done. No accounts, no cloud services
- **Full history sync** — Every Claude Code project and session on your Mac is mirrored to your iPhone
- **Real-time two-way sessions** — Whatever Claude Code is doing on your Mac, you see it live on iPhone; conversations started from iPhone show up on Mac instantly
- **End-to-end encrypted** — All traffic is encrypted; the relay is a blind pipe that cannot read a single byte of your content
- **Forward secrecy** — Each session uses ephemeral keys; a leaked key cannot decrypt past sessions
- **Local-first** — All data lives on your Mac. The iPhone is just an encrypted view layer

## Quick Start

### Step 1 — Install

```bash
brew install wishworldbetter/tap/seedex-cli
```

Or via curl:

```bash
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

Supports macOS (Intel / Apple Silicon) and Linux (x86_64 / arm64).

### Step 2 — Start the background service

```bash
seedex-cli service install
seedex-cli service start
```

The service runs in the background and starts on boot.

### Step 3 — Pair your iPhone

```bash
seedex-cli qrcode
```

Open the Seedex app on your iPhone and scan the code. An encrypted channel is established, all your Mac's Claude Code history appears on your iPhone, and you can drive conversations from your phone from then on.

---

## Service Management

```bash
seedex-cli service status     # Check status
seedex-cli service stop       # Stop
seedex-cli service restart    # Restart
seedex-cli service uninstall  # Remove
```

## Upgrade

```bash
brew upgrade seedex-cli
```

## Uninstall

```bash
seedex-cli service uninstall
brew uninstall seedex-cli
```

## License

The CLI binary is distributed as proprietary closed-source software.
