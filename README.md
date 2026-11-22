# 🦉 OBlast

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-0a0c10?style=flat-square"/>
  <img src="https://img.shields.io/badge/Category-OWeb-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-2.1.0-cyan?style=flat-square"/>
</p>

> **OBlast** — OS Command Injection Scanner

---

> ⚠️ **AUTHORISED USE ONLY** — Use only on systems you own or have explicit written permission to test. Unauthorised use is illegal.

---

## 📌 Overview

OBlast is an OS command-injection scanner for authorised web application testing, probing GET, POST and header vectors. It confirms injection through echo-marker output extraction and time-based blind detection, using 40+ delimiter payloads with optional WAF-bypass variants. A dry-run mode previews payloads without sending any requests, and results export to TXT or JSON.

---

## ✨ Features

- Echo-marker command injection scanning across GET/POST/header vectors
- Time-based blind injection detection with configurable sleep
- 40+ delimiter payloads with optional WAF-bypass variants
- Quick single-payload tests and dry-run payload preview (no requests)
- Proxy and cookie support with configurable timeout
- TXT / JSON report export

---

## ⚙️ Requirements

- **Linux**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OBlast scan -u "http://target/vuln?ip=1" -p ip -c id
./OBlast blind -u "http://target/ping?host=1" -p host -s 5
./OBlast dryrun
./OBlast --help
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 275+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled.s.Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
