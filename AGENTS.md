# LibreSecOps-Grok-Build — suite agents

> Ported and melted for **Grok Build**. Not a dumb Claude clone. **Defensive only.**

**Doctrine hub:** [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md`  
**Gold filter:** Does this empower or extract? → [GOLD_HAT.md](./GOLD_HAT.md)

## How to use this suite

1. Install skills (see [QUICK_START.md](./QUICK_START.md)).
2. Keep Reality OS as the global doctrine layer.
3. Use melted skills for a first defensive pass (`threat-model-lite`, `dependency-audit`, `secrets-scan`). Use `AGENTS/secops-orchestrator.md` when you want the coordinator — it is still a stub.
4. Pair with LibreDevOps for CI/IaC dogfood.

## Agents in this repo

| Agent | File | Role | Status |
|-------|------|------|--------|
| secops-orchestrator | `AGENTS/secops-orchestrator.md` | Coordinates threat model, defaults, deps, secrets, access, logging into one defensive pass | stub |

Melted specialists: `threat-model-lite`, `dependency-audit`, `secrets-scan`. Still stubs: `secure-defaults`, `access-review`, `defensive-logging`, `incident-runbook`. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Liquid Gold

Recognize gold in LibreSecOps-Claude-Code → strip Claude residue → integrate with Grok skills / `.grok/` / MCP → dogfood.

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreSecOps-Grok-Build](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code)
- https://ormus.solutions
