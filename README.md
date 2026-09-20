# LibreSecOps-Grok-Build

**Defensive SecOps skills and agents for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code), not a dumb copy.

> Status: **public v0.1** — three skills melted (`threat-model-lite`, `dependency-audit`, `secrets-scan`); the rest are honest stubs. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).  
> **Scope:** defensive only — hardening, review, runbooks. No exploit recipes, no attack PoCs.

## Why this exists

DevOps without SecOps is incomplete. LibreSecOps owns defensive security patterns for Claude Code. Grok Build needs the same *job* with Grok-native skills — paired with [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build). This repo counts only what it has melted.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md) for clone, dogfood, project-local, and user-global paths.

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git
cd LibreSecOps-Grok-Build
# Dogfood: .grok/skills/ already has the skill bodies.
# Other project: cp -R skills/* /path/to/your-project/.grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first.

## Depth (honest)

| Artifact | This repo now | Upstream Claude |
|----------|---------------|-----------------|
| Skills | 3 melted + 4 stubs | Proof the job exists; not our inventory |
| Agents | 1 stub (`secops-orchestrator`) | Proof the job exists; not our inventory |
| Plugins | 1 core bundle stub | Proof the job exists; not our inventory |

Melted means L3–L4 operable playbooks (when-to-use, checks, example, output shape) — not L5 production IR. Do not paste Claude plugin/agent/command totals here. Update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) when something melts.

## Skills

| Skill | Status | Job |
|-------|--------|-----|
| threat-model-lite | melted | Lightweight threat model (assets, actors, boundaries, controls) |
| dependency-audit | melted | Dependency risk review (advisories, pins, no CVE PoCs) |
| secrets-scan | melted | Secret smell detection + hygiene (never print values) |
| secure-defaults | stub | Secure-by-default review |
| access-review | stub | AuthZ / least-privilege review |
| incident-runbook | stub | Defensive incident runbook outline |
| defensive-logging | stub | Security-relevant logging |

Agent: `AGENTS/secops-orchestrator.md` — stub coordinator for a full defensive pass.

## Layout (Grok Build)

```
skills/                 # canonical SKILL.md bodies
AGENTS/                 # suite agents
docs/                   # DEPTH_MATRIX, MELT_RULES
.grok/skills/           # dogfood copy of skills/ (keep in sync)
.grok/plugins/          # optional plugin bundle stub
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? A finding that only scares without a control extracts. A finding that teaches a reusable control, and never leaks a secret, empowers.

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreSecOps-Grok-Build](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
