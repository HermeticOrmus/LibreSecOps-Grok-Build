# LibreSecOps-Grok-Build

**Defensive SecOps skills and agents for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code), not a dumb copy.

> Status: **v0 public scaffold** — honest stubs. Melt depth next.  
> **Scope:** defensive only — hardening, review, runbooks. No exploit recipes, no attack PoCs.

## Why this exists

DevOps without SecOps is incomplete. LibreSecOps owns defensive security patterns for Claude Code. Grok Build needs the same *job* with Grok-native skills — paired with [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build).

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md).

```bash
mkdir -p .grok/skills
cp -R skills/* .grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first.

## Depth matrix (honest)

| Artifact | v0 scaffold | Upstream Claude (proof) |
|----------|-------------|-------------------------|
| Skills (melted bodies) | 7 stubs → fill next | see upstream suite |
| Agents | 1 (`secops-orchestrator`) | upstream agents |

Counts on the right are **upstream proof**, not this repo's claim until melted.

## First skills

| Skill | Job |
|-------|-----|
| threat-model-lite | Lightweight threat model |
| secure-defaults | Secure-by-default review |
| dependency-audit | Dependency risk review |
| secrets-scan | Secret smell detection (no values printed) |
| access-review | AuthZ / least-privilege review |
| incident-runbook | Defensive incident runbook outline |
| defensive-logging | Security-relevant logging |

Agent: `AGENTS/secops-orchestrator.md` — full defensive pass.

## Layout (Grok Build)

```
skills/                 # install into .grok/skills or ~/.grok/skills
AGENTS/                 # suite agents
.grok/plugins/          # optional plugin bundle
docs/                   # DEPTH_MATRIX, MELT_RULES
```

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract?

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- Sibling: [LibreUIUX-Grok-Build](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build)
- Skills packs: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
