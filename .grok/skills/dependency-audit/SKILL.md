---
name: dependency-audit
description: Dependency risk review for Grok Build projects. Advisory-focused, not exploit development.
---

# Dependency Audit

Reduce supply-chain risk.

## Steps
1. Inventory direct and notable transitive deps.
2. Check known advisories / lockfile freshness.
3. Prefer maintained packages; pin versions.
4. Plan upgrades with regression checks.
5. Do not include exploit PoCs for CVEs.
