---
name: defensive-logging
description: Security-relevant logging guidance for Grok Build. Privacy-aware.
---

# Defensive Logging

Log enough to investigate; not enough to leak.

## Steps
1. Log auth events, admin actions, and high-risk mutations.
2. Include correlation IDs; exclude secrets and PII where possible.
3. Protect log integrity and access.
4. Define retention and alert hooks.
5. Never log passwords, tokens, or full card data.
