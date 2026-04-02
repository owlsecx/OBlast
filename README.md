# 🦉 OBlast

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux%20%2F%20Windows-informational?style=flat-square&logo=linux&logoColor=white&color=0a0c10"/>
  <img src="https://img.shields.io/badge/Category-OWeb%20%2F%20Command%20Injection-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0-cyan?style=flat-square"/>
</p>

> **OBlast** is an OS command injection scanner — echo-marker output extraction, time-based blind detection, header injection, 40+ delimiter payloads, WAF bypass variants, a 24-command built-in library, and TXT report export.

---

> ⚠️ **AUTHORISED SECURITY TESTING USE ONLY** — Use only on systems you own or have explicit written consent to test.

---

## 📌 Overview

OBlast tests web parameters and HTTP headers for OS command injection (CMDi) vulnerabilities. It supports both reflected injection (echo-marker output extraction) and blind injection (time-based sleep detection), covering Unix and Windows targets. All confirmed findings are saved as structured TXT reports to `oblast_reports/`.

---

## 🖥️ Modules

| # | Module | Description |
|---|--------|-------------|
| **[1] Full Scan** | Iterates core delimiters with echo-marker technique — injects `echo OBLAST_S_` + command + `echo OBLAST_E_` and extracts reflected output between markers. Stops on first confirmed finding |
| **[2] Blind Injection** | Tests 8 sleep-based payloads (Unix and Windows) and measures response time against baseline. Confirms injection if delay exceeds 75% of the configured sleep duration |
| **[3] Header Injection** | Tests 7 HTTP headers (User-Agent, Referer, X-Forwarded-For, X-Client-IP, X-Real-IP, Host, Cookie) with echo-marker payloads across 4 delimiters per header |
| **[4] Quick Inject** | Single command, single delimiter, instant result — echo-marker confirmation with custom payload |
| **[5] Payload Browser** | View all delimiters, the full command library, WAF bypass samples — with optional export to `oblast_reports/oblast_payloads_*.txt` |

---

## 🔀 Delimiter Library (40+ variants)

| Category | Delimiters |
|----------|-----------|
| **Unix** | `;` `&&` `\|\|` `\|` `\n` `%0a` `%0A` `` ` `` `$(` `)` |
| **Windows** | `&` `^` `^^` |
| **URL encoded** | `%3b` `%26%26` `%7c` `%0a%0d` |
| **Blind / IFS** | `;sleep${IFS}5;` `&&sleep${IFS}5&&` `\|sleep${IFS}5\|` |

---

## 🛡️ WAF Bypass Techniques

Three bypass methods are applied per command variant when WAF bypass mode is enabled:

| Technique | Example |
|-----------|---------|
| **IFS space substitution** | `cat${IFS}/etc/passwd` · `cat$IFS$9/etc/passwd` · `cat%09/etc/passwd` |
| **Hex encoding** | `$'\x63\x61\x74\x20\x2f\x65\x74\x63\x2f\x70\x61\x73\x73\x77\x64'` |
| **String concatenation** | `c''at` · `i''d` · `l''s` |

---

## 📋 Built-in Command Library (24 commands)

### Unix / Linux
| # | Command | Description |
|---|---------|-------------|
| 1 | `id` | User identity |
| 2 | `whoami` | Current user |
| 3 | `uname -a` | Kernel info |
| 4 | `cat /etc/passwd` | User accounts |
| 5 | `ls -la /` | Root directory |
| 6 | `pwd` | Working directory |
| 7 | `env` | Environment variables |
| 8 | `hostname` | Hostname |
| 9 | `ifconfig` | Network interfaces |
| 10 | `ip a` | IP addresses |
| 11 | `ps aux` | Running processes |
| 12 | `netstat -an` | Network connections |
| 13 | `cat /etc/shadow` | Password hashes |
| 14 | `cat /etc/hosts` | Hosts file |
| 15 | `find / -perm -4000 -type f 2>/dev/null` | SUID binaries |
| 16 | `crontab -l` | Cron jobs |
| 17 | `df -h` | Disk usage |
| 18 | `uptime` | System uptime |

### Windows
| # | Command | Description |
|---|---------|-------------|
| 19 | `whoami` | Windows user |
| 20 | `ipconfig /all` | Windows network |
| 21 | `dir C:\` | Windows C: root |
| 22 | `type C:\Windows\win.ini` | win.ini |
| 23 | `net user` | Windows users |
| 24 | `systeminfo` | Windows sysinfo |

---

## 🔍 Detection Techniques

### Echo-Marker (Reflected)
Injects timestamped markers around the command output:
```
safe_value{delim}echo OBLAST_S_{ts}{delim}COMMAND{delim}echo OBLAST_E_{ts}
```
If both markers appear in the response, the text between them is extracted and displayed as confirmed command output. HTML tags are stripped from the output.

### Time-Based (Blind)
Injects sleep commands and compares response time against baseline. Confirmation threshold: **actual delay > baseline + 75% of sleep duration**. Tests 8 payloads:

`;sleep N;` · `&&sleep N&&` · `|sleep N` · `||sleep N` · `%0asleep%20N` · `;sleep${IFS}N;` · `&ping -n N 127.0.0.1&` · `|timeout N`

---

## 📤 Reports

All confirmed findings saved to `oblast_reports/`:

| Type | Filename | Contents |
|------|----------|----------|
| Scan report | `oblast_report_YYYYMMDD_HHMMSS.txt` | Target URL, start time, payloads tested, per-finding: method, param, delimiter, technique, command, elapsed ms, full output (up to 30 lines) |
| Payload export | `oblast_payloads_YYYYMMDD_HHMMSS.txt` | All delimiters and command library |

---

## ⚙️ Requirements

- **Linux or Windows**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OBlast
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
