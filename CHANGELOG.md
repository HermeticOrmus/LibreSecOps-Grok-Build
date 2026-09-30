# Changelog

## [1.0.0] - 2026-09-30

The Grok edition: the melted skills install as a Grok plugin, and the same marketplace installs every LibreSecOps-Claude-Code plugin, pinned to one commit of the pack. The [kintsugi ledger](./LEDGER.md) records each v0 crack and its seal.

### Added

- `plugins/libre-secops-grok/`, the Grok-native plugin (`.grok-plugin/plugin.json`, version 1.0.0) with the three melted skills: `threat-model-lite`, `dependency-audit`, `secrets-scan`. Defensive only, as before.
- `.grok-plugin/marketplace.json` (`libre-secops-grok`): the Grok-native plugin plus all 33 LibreSecOps-Claude-Code plugins as remote entries pinned to pack commit `a874d37f7d9b5ea6c27f4fc5185dd2dc4fdc83f7`.
- `scripts/pin-pack.sh`: re-pins the pack entries to the pack's `main`, adds new pack plugins, drops removed ones, and prints the diff; `--check` fails on an unreachable SHA or a changed plugin list.
- `.github/workflows/validate.yml`: `grok plugin validate`, the dogfood copy check, the doc install-line check, the pin check, and an install of every entry into a clean `GROK_HOME`.
- Issue forms for feedback, routing misses and plugin proposals, with the `feedback`, `routing-miss` and `plugin-proposal` labels.
- [LEDGER.md](./LEDGER.md), [stubs/README.md](./stubs/README.md), and "Ways to contribute" in [CONTRIBUTING.md](./CONTRIBUTING.md).

### Changed

- Install is `grok plugin marketplace add HermeticOrmus/LibreSecOps-Grok-Build` then `grok plugin install libre-secops-grok@libre-secops-grok --trust`. The folder copy still works from the new path, `plugins/libre-secops-grok/skills/*`.
- Melted skills moved from `skills/` to `plugins/libre-secops-grok/skills/`; the four stubs moved to `stubs/`. The `.grok/skills/` dogfood copy stays and matches both.
- The v0 bundle stub `.grok/plugins/libresecops-core/` moved to `stubs/libresecops-core/`, marked superseded.
- README gains the family header, the marketplace install, the real Depth table, and a note on the three pack plugins written for authorized offensive work; QUICK_START, AGENTS.md, DEPTH_MATRIX and MELT_RULES follow the new paths.

### Fixed

- Stubs no longer install as if they were playbooks: their descriptions start "Stub, not a playbook." and name the pack plugin that holds the real depth.
- The v0 plugin folder installed as an unversioned plugin with no skills; the new plugin validates with its three skills.
- The Gold Hat and suite links at the foot of each melted skill were relative and broke in the `.grok/skills` copy; they are absolute now and resolve from an installed plugin too.

### Upgrading from v0

- If you copied `skills/*` into a project or `~/.grok/skills/`, remove the four stub folders from that copy, or switch to the marketplace install so `grok plugin update` brings changes.
- Paths that pointed at `skills/<name>` now point at `plugins/libre-secops-grok/skills/<name>` (melted) or `stubs/<name>` (stubs).
- Installing every marketplace entry also installs `penetration-testing`, `red-team-operations` and `bug-bounty-methodology`. Install those only with written authorization for the target.

## [0.1.0] — 2026-09-20

### Changed

- Melted `skills/threat-model-lite/SKILL.md`, `skills/dependency-audit/SKILL.md`, and `skills/secrets-scan/SKILL.md` into usable Grok skills (when-to-use, steps, checks, examples, output shape). Dogfood copies under `.grok/skills/` match.
- Rewrote [QUICK_START.md](./QUICK_START.md) for a clean-machine install (<5 min) with paths that exist in this repo.
- Updated [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md): 3 melted, 4 stub skills, 1 stub agent. No Claude inventory counts. Melted = L3–L4 operable, not L5.
- Suite footers on README, QUICK_START, AGENTS.md, DEPTH_MATRIX, and melted skills now link Reality OS plus the sibling Libre*-Grok-Build packs.
- Gold Hat applied in melted skills: teach the control; never print secrets; refuse exploit steps.

## [0.0.1] — 2026-09-19

### Added

- Public scaffold for libresecops-Grok-Build (v0 stubs).
- Stub SKILL.md for first skills + suite orchestrator agent.
- README, LICENSE (MIT), GOLD_HAT, QUICK_START, CONTRIBUTING, SECURITY.
- Depth matrix + melt rules docs.

### Notes

- Honest stubs — not fake upstream depth counts. Melt next.
