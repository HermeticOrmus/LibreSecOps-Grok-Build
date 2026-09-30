---
name: access-review
description: "Stub, not a playbook. AuthZ and least-privilege access review for Grok Build. Defensive. Real depth: the identity-access-management plugin, grok plugin install identity-access-management@libre-secops-grok --trust."
---

# Access Review

Stub, not a playbook. Real depth: the [`identity-access-management`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/identity-access-management) plugin from LibreSecOps-Claude-Code. Install it from this marketplace: `grok plugin install identity-access-management@libre-secops-grok --trust`.

Who can do what?

## Steps
1. List roles and permissions.
2. Check for over-broad admin / wildcard grants.
3. Prefer scoped tokens and short TTL.
4. Review break-glass procedures.
5. Recommend concrete reductions in privilege.
