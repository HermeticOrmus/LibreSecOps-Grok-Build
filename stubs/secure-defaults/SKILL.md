---
name: secure-defaults
description: "Stub, not a playbook. Secure-by-default review for apps and services on Grok Build. Hardening only. Real depth: the security-hardening plugin, grok plugin install security-hardening@libre-secops-grok --trust."
---

# Secure Defaults

Stub, not a playbook. Real depth: the [`security-hardening`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/security-hardening) plugin from LibreSecOps-Claude-Code. Install it from this marketplace: `grok plugin install security-hardening@libre-secops-grok --trust`.

Prefer safe defaults.

## Steps
1. AuthN/AuthZ: fail closed; least privilege.
2. Transport: TLS; HSTS where appropriate.
3. Cookies/sessions: Secure, HttpOnly, SameSite.
4. Input handling: validate; encode on output.
5. List misconfigurations to fix — no exploit walkthroughs.
