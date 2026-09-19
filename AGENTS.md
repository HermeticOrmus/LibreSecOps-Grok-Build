# LibreSecOps-Grok-Build — suite agents

> Ported and melted for **Grok Build**. Not a dumb Claude clone. **Defensive only.**

**Doctrine hub:** [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md`  
**Gold filter:** Does this empower or extract? → [GOLD_HAT.md](./GOLD_HAT.md)

## How to use this suite

1. Install skills (see [QUICK_START.md](./QUICK_START.md)).
2. Keep Reality OS as the global doctrine layer.
3. Use suite skills for defensive SecOps; use `AGENTS/secops-orchestrator.md` for a full pass.
4. Pair with LibreDevOps for CI/IaC dogfood.

## Agents in this repo

| Agent | File | Role |
|-------|------|------|
| secops-orchestrator | `AGENTS/secops-orchestrator.md` | Coordinates threat model, defaults, deps, secrets, access, logging into one defensive pass |

## Liquid Gold

Recognize gold in LibreSecOps-Claude-Code → strip Claude residue → integrate with Grok skills / `.grok/` / MCP → dogfood.
