# 🛡️ XSStrike - Practical Guide for XSS Detection in Kali 2026

![XSStrike Banner](https://github.com/s0md3v/XSStrike/raw/main/static/logo.png)

**XSStrike** is an advanced Cross-Site Scripting (XSS) detection tool equipped with an intelligent payload generator, a powerful fuzzing engine, and a fast crawler.

---

## 📋 Table of Contents

- [Installation](#-installation)
- [Basic Commands](#-basic-commands)
- [Practical Scenarios](#-practical-scenarios)
- [Real-World Use Case - Reflected XSS on Pikachu](#-real-world-use-case---reflected-xss-on-pikachu)
- [Limitations](#-limitations)
- [Resources](#-resources)

---

## 🔧 Installation

In Kali 2026, XSStrike is included in the official repositories:

```bash
# Simple installation
sudo apt update
sudo apt install xsstrike -y

# Verify installation
xsstrike -h
Required dependencies:

· Python 3
· python3-fuzzywuzzy
· python3-requests
· python3-tld

---

🎯 Basic Commands

1. Simple URL scan (GET)

```bash
xsstrike -u "http://target.com/search.php?q=test"
```

2. POST request scan

```bash
xsstrike -u "http://target.com/search.php" --data "q=test"
```

3. Path injection

```bash
xsstrike -u "http://target.com/search/test" --path
```

4. Crawling and automated testing

```bash
xsstrike -u "http://target.com" --crawl -l 2
```

5. Custom payloads

```bash
xsstrike -u "http://target.com/page.php?q=test" -f /path/to/payloads.txt
```

6. Discover hidden parameters

```bash
xsstrike -u "http://target.com/page.php" --params
```

7. Proxy usage

```bash
xsstrike -u "http://target.com" --proxy http://127.0.0.1:8080
```

8. Custom headers

```bash
xsstrike -u "http://target.com" --headers "Cookie: session=abc123\nUser-Agent: Mozilla/5.0"
```

---

🔍 Practical Scenarios

Scenario 1: Reflected XSS (GET)

```bash
# Test vulnerable endpoint
xsstrike -u "http://target.com/vuln.php?name=test" --skip-dom
```

What it does: XSStrike analyzes the response, detects the HTML context, and generates customized payloads.

Scenario 2: Reflected XSS (POST)

```bash
# Test POST form with authentication
xsstrike -u "http://target.com/login.php" --data "username=
