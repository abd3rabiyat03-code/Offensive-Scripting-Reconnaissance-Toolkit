

## What is this?

This is Phase 2 of our network security programming project. We built an offensive security toolkit that covers three main areas: automated reconnaissance, SSH/FTP interaction, and a sandboxed educational payload demonstration.

Everything here is meant to run in a **local lab environment only**. No external systems were targeted — not during development, not during testing, not ever. This is purely for learning purposes inside a controlled setup.

---

## Project Structure

```
├── recon_tool.py          # Reconnaissance module
├── ssh_interaction.py     # SSH & FTP interaction module
├── sandboxed_payload.py   # Reverse shell payload (localhost only)
├── listener.py            # Local listener for the payload demo
└── README.md
```

---

## What each file does

### `recon_tool.py` — Reconnaissance Module
This script automates the information-gathering phase. It handles:
- **DNS enumeration** — queries different record types (A, MX, NS, TXT)
- **WHOIS lookups** — pulls registration info for a given domain
- **Banner grabbing** — connects to open ports and reads service banners
- **HTTP header inspection** — checks what a web server reveals about itself
- **Subdomain brute-forcing** — tries a wordlist to discover hidden subdomains

Results are automatically saved to a structured output file so you don't have to copy-paste anything manually.

---

### `ssh_interaction.py` — SSH & FTP Interaction Module
Built with `paramiko` and `ftplib`. This module can:
- Connect to SSH servers using **both password and key-based authentication**
- Execute remote commands over SSH and print the output
- Transfer files over **SFTP** (upload and download)
- Connect to FTP servers and navigate directories
- Detect and handle repeated failed login attempts (rate-limiting logic)

---

### `sandboxed_payload.py` — Educational Payload
A reverse shell that connects back to a local listener. This exists purely to demonstrate how payloads work in a controlled environment.

⚠️ **This only connects to `127.0.0.1` (localhost).** It is hardcoded to never reach outside your machine. The ethical-use disclaimer is written directly in the source code comments.

---

### `listener.py` — Local Listener
A simple TCP listener that waits for the reverse shell connection. Run this first on the same machine, then trigger the payload — you'll get an interactive shell session entirely within localhost.

---

## How to run it (local lab setup)

**Requirements:**
```bash
pip install paramiko dnspython python-whois requests
```

**Step 1 — Start the listener (for payload demo):**
```bash
python listener.py
```

**Step 2 — Run recon against a test target:**
```bash
python recon_tool.py --target <your-lab-domain-or-IP>
```

**Step 3 — Test SSH/FTP interaction:**
```bash
python ssh_interaction.py --host <lab-server-IP> --user <username>
```

**Step 4 — Trigger the sandboxed payload (optional demo):**
```bash
python sandboxed_payload.py
```

> Make sure everything is running on your local machine or an isolated lab VM. Do not point any of these tools at systems you don't own or have written permission to test.

---

## Ethical Use Policy

This toolkit was built as an academic exercise for understanding offensive security concepts — not for actual offensive use. Every technique here has a defensive mirror: understanding how recon works helps you detect it; understanding how reverse shells behave helps you block them.

**Usage rules we follow (and you should too):**
- Only run this in a sandboxed or local lab environment
- Never test against real-world targets without explicit written permission
- This code is for educational purposes only

Any misuse of this toolkit is the sole responsibility of the person running it. The authors do not condone unauthorized access to computer systems.

---

## Phase 1 Integration

This builds on the port scanner from Phase 1. The recon module picks up where the scanner left off — once you've identified open ports, banner grabbing and service fingerprinting give you a fuller picture of what's running.

---

## Notes

- Tested on: Python 3.10+, Windows 10/11 and Linux (Ubuntu 22.04)
- All test runs were performed on localhost or a local VirtualBox lab
- Screenshots of execution are included in the submitted PDF report

---

*Built for academic purposes — University of Petra, 2025–2026*
