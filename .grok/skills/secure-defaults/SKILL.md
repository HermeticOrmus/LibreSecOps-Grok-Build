---
name: secure-defaults
description: Secure-by-default review for apps and services on Grok Build. Hardening only.
---

# Secure Defaults

Prefer safe defaults.

## Steps
1. AuthN/AuthZ: fail closed; least privilege.
2. Transport: TLS; HSTS where appropriate.
3. Cookies/sessions: Secure, HttpOnly, SameSite.
4. Input handling: validate; encode on output.
5. List misconfigurations to fix — no exploit walkthroughs.
