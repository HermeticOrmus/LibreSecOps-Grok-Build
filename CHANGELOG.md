# Changelog

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
