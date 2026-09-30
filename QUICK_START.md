# Quick Start — LibreSecOps for Grok Build

> From a clean machine to one defensive review in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

Gold Hat: [GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? Teach the control while you find the gap. Never print secret values. Never produce exploit steps.

## Prerequisites

- Grok Build (`grok --version` prints a version)
- `git` and `jq` for the clone paths and the install-everything loop
- A service or repo you own, **or** this repo as the working tree (authorized only)

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```text
plugins/libre-secops-grok/                        # the Grok-native plugin
plugins/libre-secops-grok/skills/<name>/SKILL.md  # melted skill bodies (copy these for the manual path)
stubs/<name>/SKILL.md                             # stub cues; not installed
AGENTS/secops-orchestrator.md                     # stub coordinator
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok-plugin/marketplace.json                     # the plugin + every pack plugin, pinned
.grok/skills/<name>/SKILL.md                      # dogfood copy of the plugin skills and stubs
stubs/libresecops-core/                           # v0 plugin bundle stub, kept as the record
```

Melted (usable now): `threat-model-lite`, `dependency-audit`, `secrets-scan`, in `plugins/libre-secops-grok/skills/`.
Still stubs: `secure-defaults`, `access-review`, `incident-runbook`, `defensive-logging`, plus the orchestrator. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Marketplace (recommended)

```bash
grok plugin marketplace add HermeticOrmus/LibreSecOps-Grok-Build
grok plugin install libre-secops-grok@libre-secops-grok --trust
grok plugin details libre-secops-grok
```

Grok installs a plugin only with `--trust`, because a plugin can run hooks, MCP servers and skills on your machine. Without it, `grok plugin install` stops and asks you to re-run with the flag.

The same marketplace lists every [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) plugin, pinned to one commit of the pack. Install the ones your work needs by name:

```bash
grok plugin install threat-modeling@libre-secops-grok --trust
grok plugin install supply-chain-security@libre-secops-grok --trust
```

Or install every entry:

```bash
for p in $(grok plugin list --json --available | jq -r '.[] | select(.marketplace == "libre-secops-grok" and .status == "available") | .name'); do
  grok plugin install "$p@libre-secops-grok" --trust
done
```

Every entry includes the pack plugins written for authorized offensive work (`penetration-testing`, `red-team-operations`, `bug-bounty-methodology`). Install those only when you hold written authorization for the target; the loop above installs them too.

`libre-secops-hooks` is format-compatible with Grok, but its behavior inside a Grok session is not verified yet (see [LEDGER.md](./LEDGER.md)). Skip it if you only want skills and agents.

To pick up a new pin later: `grok plugin marketplace update`, then `grok plugin update`.

### B. Dogfood this repo

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git
cd LibreSecOps-Grok-Build
# A copy of the skills and stubs is already at .grok/skills/. Open this folder in Grok Build.
```

### C. Copy into your project

The v0 path, for a project that should carry the skill files itself.

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git ~/LibreSecOps-Grok-Build
cd /path/to/your-project
mkdir -p .grok/skills
cp -R ~/LibreSecOps-Grok-Build/plugins/libre-secops-grok/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/threat-model-lite/SKILL.md
test -f .grok/skills/dependency-audit/SKILL.md
test -f .grok/skills/secrets-scan/SKILL.md
ls .grok/skills
```

You should see three skill directories, matching `plugins/libre-secops-grok/skills/` in this repo. The stubs are not copied: they are pointers to pack plugins, not skills.

### D. User-global copy

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git ~/LibreSecOps-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreSecOps-Grok-Build/plugins/libre-secops-grok/skills/* ~/.grok/skills/
```

Same three `test -f` checks as C, under `~/.grok/skills/`.

### Upgrading from v0

If you copied `skills/*` into a project or `~/.grok/skills/`, that copy holds all seven folders, stubs included. Remove the four stub folders (`secure-defaults`, `access-review`, `incident-runbook`, `defensive-logging`) from the copy, or replace the copy with path A so updates arrive through `grok plugin update`.

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

- [ ] `grok plugin list` shows `libre-secops-grok` (path A), or the three melted skill files exist at the copy path you chose (C or D)
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
