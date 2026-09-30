---
name: defensive-logging
description: "Stub, not a playbook. Security-relevant logging guidance for Grok Build. Privacy-aware. Real depth: the siem-log-management plugin, grok plugin install siem-log-management@libre-secops-grok --trust."
---

# Defensive Logging

Stub, not a playbook. Real depth: the [`siem-log-management`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/siem-log-management) plugin from LibreSecOps-Claude-Code. Install it from this marketplace: `grok plugin install siem-log-management@libre-secops-grok --trust`.

Log enough to investigate; not enough to leak.

## Steps
1. Log auth events, admin actions, and high-risk mutations.
2. Include correlation IDs; exclude secrets and PII where possible.
3. Protect log integrity and access.
4. Define retention and alert hooks.
5. Never log passwords, tokens, or full card data.
