# 🛡️ NOIR IDS — Intrusion Detection System

> A browser-based Linux log analyser for detecting intrusion indicators — no installation, no server, no dependencies.

**Author:** Radhesh Mutreja &nbsp;|&nbsp; **Course:** DFIS &nbsp;|&nbsp; **Version:** 2.0 Web

---

## Overview

Noir IDS is a single-file HTML tool that analyses Linux authentication and system logs for signs of malicious activity. Drop it in a browser, load a log file, and get an instant colour-coded alert feed with a one-click HTML report export.

All processing runs **entirely in your browser** — no data is ever uploaded anywhere.

---

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/your-username/noir-ids.git
cd noir-ids

# 2. Open in browser
# Windows
start noir-ids.html

# macOS
open noir-ids.html

# Linux
xdg-open noir-ids.html
```

Then:
1. **Drag & drop** a log file onto the drop zone (or click to browse)
2. Click **▶ Analyse File** for a full scan, or **📡 Live Monitor** for real-time tailing
3. Filter by severity, search alerts, then click **📊 Generate HTML Report** to export

---

## Features

| Feature | Details |
|---|---|
| 🚫 Zero installation | Single `.html` file, works fully offline |
| 🔍 15 detection patterns | SSH, sudo, PAM, user management, and more |
| 💥 Brute force detection | Configurable failed-attempt threshold per IP/user |
| 🎯 Distributed attack detection | Alerts when one user is targeted from 4+ IPs |
| 🔁 High-frequency IP tracking | Flags IPs exceeding a configurable repeat limit |
| 🌙 Suspicious hour window | Configurable time range (default 00:00–06:00) |
| 🎨 Real-time alert feed | Colour-coded by severity with raw log line preview |
| 🔎 Filter & search | Filter by severity or free-text search instantly |
| 📊 HTML report export | Self-contained styled report, opens in any browser |
| ⚙️ Configurable thresholds | All detection limits adjustable in the UI |

---

## Detection Rules

| Alert | Severity | Description |
|---|---|---|
| BRUTE FORCE / FAILED LOGIN | 🔴 HIGH | Failed SSH password attempt |
| INVALID USER ATTEMPT | 🔴 HIGH | Login with non-existent username |
| ROOT LOGIN | 🔴 HIGH | Direct root login detected |
| NEW USER CREATED | 🔴 HIGH | A new system account was created |
| USER DELETED | 🔴 HIGH | A system user account was deleted |
| BREAK-IN ATTEMPT | 🔴 HIGH | System flagged a possible intrusion |
| MAX AUTH EXCEEDED | 🔴 HIGH | Too many auth attempts from one IP |
| AUTH FAILURES DISCONNECT | 🔴 HIGH | Client disconnected after repeated failures |
| ⚠ BRUTE FORCE DETECTED | 🔴 HIGH | IP/user hit the failed attempt threshold |
| 🎯 DISTRIBUTED ATTACK | 🔴 HIGH | One user targeted from 4+ distinct IPs |
| SUDO COMMAND EXECUTED | 🟠 MEDIUM | Privilege escalation via sudo |
| AUTH FAILURE | 🟠 MEDIUM | PAM authentication failure |
| 🌙 SUSPICIOUS HOUR | 🟠 MEDIUM | Activity within suspicious hour window |
| 🔁 HIGH FREQUENCY IP | 🟠 MEDIUM | IP exceeded the repeat threshold |
| SUCCESSFUL SSH LOGIN | 🟡 LOW | User logged in via SSH password |
| SSH KEY LOGIN | 🟢 INFO | User authenticated via SSH public key |
| SESSION OPENED | 🟢 INFO | A new user session was opened |
| SESSION CLOSED | 🟢 INFO | A user session was closed |
| CONNECTION CLOSED | 🟢 INFO | SSH connection was closed |

---

## Configurable Thresholds

All thresholds are editable in the left panel before running an analysis.

| Setting | Default | Description |
|---|---|---|
| Brute force limit | `5` | Failed logins before flagging brute force |
| IP repeat limit | `10` | Total appearances before flagging an IP |
| Suspicious hour (from) | `0` | Start of suspicious window (0–23) |
| Suspicious hour (to) | `6` | End of suspicious window (0–23) |

---

## Supported Log Files

```
/var/log/auth.log       # Debian / Ubuntu
/var/log/secure         # RHEL / CentOS / Fedora
/var/log/syslog         # General system log
/var/log/messages       # General system log (RHEL/CentOS)
```

> **Tip:** If the file is permission-restricted, copy it first:
> ```bash
> sudo cp /var/log/auth.log ~/auth.log
> sudo chown $USER ~/auth.log
> ```

Both **syslog** (`Jan 12 03:45:12`) and **ISO 8601** (`2026-01-12T03:45:12`) timestamp formats are parsed automatically.

---

## Live Monitor

Live Monitor polls the selected file every 800 ms for new content, starting from the end of the file — equivalent to `tail -f`.

For monitoring actively-written system logs, pipe them to a user-accessible file first:

```bash
sudo tail -f /var/log/auth.log >> ~/live-auth.log &
# Then load ~/live-auth.log into Noir IDS and click Live Monitor
```

---

## HTML Report Export

Click **📊 Generate HTML Report** after any analysis to download a fully self-contained report including:

- Summary cards (counts by severity)
- Top 5 most frequent alert types
- Full alert table with severity filter buttons and live search
- Raw log line previews per alert

The report is a single `.html` file that works offline in any browser.

---

## Browser Compatibility

| Browser | Support |
|---|---|
| Chrome 90+ | ✅ |
| Firefox 90+ | ✅ |
| Edge 90+ | ✅ |
| Safari 15+ | ✅ |
| Internet Explorer | ❌ |

---

## Project Structure

```
noir-ids/
├── noir-ids.html   # Complete application — everything in one file
└── README.md       # This file
```

---

## Disclaimer

> Noir IDS is an **educational tool** developed as part of a Digital Forensics and Incident Response (DFIS) course project. It demonstrates log analysis and pattern-matching concepts and is **not** a production-grade security product. Do not rely on it as a sole means of intrusion detection.

---

<p align="center">
  © 2026 Radhesh Mutreja &nbsp;|&nbsp; DFIS Course Project &nbsp;|&nbsp; Educational Use Only
</p>
