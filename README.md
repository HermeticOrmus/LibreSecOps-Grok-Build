<p align="center">
  <img src="https://ormus.solutions/mascot/pixellab_liquid_to_hylian_shield.gif" alt="LibreSecOps Grok Build" width="128" style="image-rendering: pixelated;" />
</p>

<h1 align="center">LibreSecOps Grok Build</h1>

<p align="center">
  <em>Defensive security operations for Grok Build: Grok-native skills plus every LibreSecOps pack plugin, from one marketplace</em>
</p>

<p align="center">
  <a href="https://github.com/HermeticOrmus/LibreSecOps-Grok-Build/stargazers"><img src="https://img.shields.io/github/stars/HermeticOrmus/LibreSecOps-Grok-Build?style=flat-square&color=aa8142" alt="Stars" /></a>
  <a href="https://github.com/HermeticOrmus/LibreSecOps-Grok-Build/blob/main/LICENSE"><img src="https://img.shields.io/github/license/HermeticOrmus/LibreSecOps-Grok-Build?style=flat-square&color=aa8142" alt="License" /></a>
  <a href="https://github.com/HermeticOrmus/LibreSecOps-Grok-Build/commits"><img src="https://img.shields.io/github/last-commit/HermeticOrmus/LibreSecOps-Grok-Build?style=flat-square&color=aa8142" alt="Last Commit" /></a>
  <img src="https://img.shields.io/badge/Security-aa8142?style=flat-square&logo=hackthebox&logoColor=white" alt="Security" />
  <img src="https://img.shields.io/badge/Grok_Build-aa8142?style=flat-square&logo=x&logoColor=white" alt="Grok Build" />
</p>

---

**Defensive SecOps skills and agents for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code), not a dumb copy.

> Status: **v1.0.0**. Three skills are melted into the Grok-native plugin `libre-secops-grok` (`threat-model-lite`, `dependency-audit`, `secrets-scan`). The other four are honest stubs in [stubs/](./stubs/), each pointing at the pack plugin that holds the real depth. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) and the [kintsugi ledger](./LEDGER.md).  
> **Scope:** defensive only — hardening, review, runbooks. No exploit recipes, no attack PoCs.

## Why this exists

DevOps without SecOps is incomplete. LibreSecOps owns defensive security patterns for Claude Code. Grok Build needs the same *job* with Grok-native skills — paired with [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build). This repo counts only what it has melted.

## Install

One marketplace brings both layers: the Grok-native plugin melted here, and every plugin of the [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) pack, pinned to one commit of the pack. Grok reads the pack plugins as they are.

```bash
grok plugin marketplace add HermeticOrmus/LibreSecOps-Grok-Build
grok plugin install libre-secops-grok@libre-secops-grok --trust
```

Grok installs a plugin only with `--trust`, because a plugin can run hooks, MCP servers and skills on your machine. Read what you trust: each entry's source is linked in [.grok-plugin/marketplace.json](./.grok-plugin/marketplace.json).

Then add the pack plugins your work needs, for example:

```bash
grok plugin install threat-modeling@libre-secops-grok --trust
grok plugin install secrets-management@libre-secops-grok --trust
```

The scope line above covers the Grok-native plugin. The pack also carries plugins written for authorized offensive work (`penetration-testing`, `red-team-operations`, `bug-bounty-methodology`). Install those only when you hold written authorization for the target.

[QUICK_START.md](./QUICK_START.md) has the loop that installs every entry, the dogfood clone, and the manual copy path. From a clone:

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git
cd LibreSecOps-Grok-Build
# Dogfood: .grok/skills/ holds a copy of the skill bodies and stubs.
# Other project: cp -R plugins/libre-secops-grok/skills/* /path/to/your-project/.grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first.

## Depth (honest)

| Artifact | This repo now | Where |
|----------|---------------|-------|
| Grok-native skills | 3 melted | `plugins/libre-secops-grok/skills/` |
| Stub skills | 4, not installed | `stubs/`, each names its pack plugin |
| Agents | 1 stub (`secops-orchestrator`), not installed | `AGENTS/` |
| Plugins in the marketplace | 1 Grok-native + 33 pack entries | `.grok-plugin/marketplace.json`, pinned to one pack commit |

Melted means L3–L4 operable playbooks (when-to-use, checks, example, output shape) — not L5 production IR. Do not paste Claude plugin/agent/command totals here. Update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) when something melts.

Pack entries are LibreSecOps-Claude-Code plugins installed through this marketplace. They are not melted here, and they are not counted as this repo's skills. Run `scripts/pin-pack.sh` when the pack changes.

## Skills

| Skill | Status | Job | Pack plugin |
|-------|--------|-----|-------------|
| threat-model-lite | melted | Lightweight threat model (assets, actors, boundaries, controls) | melted from `threat-modeling` |
| dependency-audit | melted | Dependency risk review (advisories, pins, no CVE PoCs) | melted from `supply-chain-security` |
| secrets-scan | melted | Secret smell detection + hygiene (never print values) | melted from `secrets-management` |
| secure-defaults | stub | Secure-by-default review | real depth in `security-hardening` |
| access-review | stub | AuthZ / least-privilege review | real depth in `identity-access-management` |
| incident-runbook | stub | Defensive incident runbook outline | real depth in `incident-response` |
| defensive-logging | stub | Security-relevant logging | real depth in `siem-log-management` |

Agent: `AGENTS/secops-orchestrator.md` — stub coordinator for a full defensive pass.

## Layout (Grok Build)

```text
plugins/libre-secops-grok/  # the Grok-native plugin: manifest + melted SKILL.md bodies
stubs/                      # stub skills + the v0 bundle stub; not installed
AGENTS/                     # suite agents
docs/                       # DEPTH_MATRIX, MELT_RULES
scripts/pin-pack.sh         # re-pins the pack entries to the pack's main
.grok-plugin/               # marketplace: the plugin + every pack plugin, pinned
.grok/skills/               # dogfood copy of the plugin skills and stubs (CI checks it)
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Kintsugi ledger

Every crack found in v0 and how this release seals it, with the file that shows the seal: [LEDGER.md](./LEDGER.md).

## Feedback and contributing

Tell us what worked and what is missing with the [feedback form](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build/issues/new?template=feedback.yml). When Grok picks the wrong skill, file a [routing miss](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build/issues/new?template=routing-miss.yml). Ways to contribute are in [CONTRIBUTING.md](./CONTRIBUTING.md). Security reports stay private: see [SECURITY.md](./SECURITY.md).

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
