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
xsstrike -u "http://target.com/login.php" --data "username=admin&password=123" --headers "Cookie: PHPSESSID=abc123"
```

Scenario 3: Stored XSS

```bash
# Test endpoint that saves to database
xsstrike -u "http://target.com/comments.php" --data "comment=test&submit=1" --skip-dom --skip
```

⚠️ Note: XSStrike may not automatically detect Stored XSS since it doesn't run multi-step workflows. Manual verification is required after scanning.

Scenario 4: DOM-Based XSS

```bash
# Test DOM endpoint
xsstrike -u "http://target.com/dom.php" --skip-dom
```

⚠️ Limitation: DOM-based XSS is not always detected since it runs on the client-side (in the browser).

---

💻 Real-World Use Case - Reflected XSS on Pikachu

I tested XSStrike on the Reflected XSS (GET) vulnerability from the Pikachu lab.

Step 1: Identify vulnerable endpoint

```
http://127.0.0.1/pikachu/vul/xss/xss_reflected_get.php?message=kobe&submit=submit
```

Step 2: Scan with XSStrike

```bash
xsstrike -u "http://127.0.0.1/pikachu/vul/xss/xss_reflected_get.php?message=kobe&submit=submit" --skip --skip-dom
```

Step 3: Payload generated and validated

```
<detAiLs%0DoNtoGgle%0A=%0Aconfirm()//
```

Step 4: Payload in browser

```
http://127.0.0.1/pikachu/vul/xss/xss_reflected_get.php?message=%3CdetAiLs%0doNtoGgle%0a=%0aconfirm()//&submit=submit
```

Result: The payload executed confirm() in the browser, confirming Reflected XSS.

---

⚠️ Limitations

XSS Type XSStrike Detection Explanation
Reflected XSS ✅ Good Detects effectively, generates contextual payloads
Stored XSS ❌ Weak Doesn't run multi-step workflows automatically
DOM-Based XSS ⚠️ Partial Runs client-side, server-side scanner can't execute
False positives ⚠️ Possible After patching, XSStrike may still report non-existent vulnerabilities

Conclusion: XSStrike is excellent for Reflected XSS but does not replace manual testing.

---

📚 Resources

· Official Documentation
· XSS Payload List
· Intigriti - Hacker tools: XSStrike

---

📌 Disclaimer: This guide is for educational purposes in authorized environments only. Do not use these techniques on systems without written permission.
