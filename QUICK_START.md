# Quick Start — LibreSecOps for Grok Build

> From a clean machine to one defensive review in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

Gold Hat: [GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? Teach the control while you find the gap. Never print secret values. Never produce exploit steps.

## Prerequisites

- `git`
- Grok Build installed and able to see skills under `.grok/skills/` or `~/.grok/skills/`
- A service or repo you own, **or** this repo as the working tree (authorized only)

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```
skills/<name>/SKILL.md                 # canonical skill bodies (copy these)
AGENTS/secops-orchestrator.md          # stub coordinator
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok/skills/<name>/SKILL.md           # dogfood copy; must match skills/
.grok/plugins/libresecops-core/        # plugin stub; not required for first run
```

Melted (usable now): `skills/threat-model-lite/SKILL.md`, `skills/dependency-audit/SKILL.md`, `skills/secrets-scan/SKILL.md`.
Still stubs: `secure-defaults`, `access-review`, `incident-runbook`, `defensive-logging`, plus the orchestrator. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Dogfood this repo (fastest)

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git
cd LibreSecOps-Grok-Build
# Skills are already at .grok/skills/ — open this folder in Grok Build.
```

### B. Install into your project

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git ~/LibreSecOps-Grok-Build
cd /path/to/your-project
mkdir -p .grok/skills
cp -R ~/LibreSecOps-Grok-Build/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/threat-model-lite/SKILL.md
test -f .grok/skills/dependency-audit/SKILL.md
test -f .grok/skills/secrets-scan/SKILL.md
ls .grok/skills
```

You should see seven skill directories, matching `skills/` in this repo.

### C. User-global

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git ~/LibreSecOps-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreSecOps-Grok-Build/skills/* ~/.grok/skills/
```

Same three `test -f` checks as B, under `~/.grok/skills/`.

### Optional orchestrator (still a stub)

Copy `AGENTS/secops-orchestrator.md` only when you want a multi-skill defensive pass. It coordinates; it does not add specialist depth the stubs do not have. Merge into project `AGENTS.md` / `.grok/AGENTS.md` — do not overwrite Reality OS doctrine.

## First-run teach cue

In Grok Build, on a service you own:

1. **Model** — "Run threat-model-lite: name the user job, assets, actors, and trust boundaries. STRIDE as questions. Rank residual risk. No exploit steps."
2. **Deps** — "Run dependency-audit on the lockfile. Cite advisory IDs or mark unverified. Pin and plan upgrades. No CVE PoCs."
3. **Secrets** — "Run secrets-scan for smell patterns. Report path and pattern type only. Redact values. Prefer a manager; rotate if exposure is plausible."

You used melted LibreSecOps depth on Grok — not a Claude paste, not a fake plugin count.

## Hard rules

- Defensive guidance only.
- No exploit steps, payloads, or attack scripts.
- Never embed or echo real secrets (output `REDACTED`).

## Smoke checklist

- [ ] The three melted skill files exist at the install path you chose
- [ ] Grok can see `threat-model-lite`, `dependency-audit`, `secrets-scan`
- [ ] One threat model with job, boundaries, ranked controls (no attack procedure)
- [ ] One dependency note with versions and next actions (or explicit unverified)
- [ ] One secrets pass with paths + types only — no secret values, no exploit content

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreSecOps-Grok-Build](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof (upstream, not this inventory): [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code)
- https://ormus.solutions
