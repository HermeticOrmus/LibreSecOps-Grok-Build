# Depth matrix

Update this table when melting. Status words mean what they say:

| Status | Meaning |
|--------|---------|
| stub | Thin cue only. Usable as a reminder, not a playbook. |
| melted | Operable Grok skill (L3–L4): when-to-use, steps, measurable checks, worked example, output shape. Not an L5 IR shop. |

Never copy Claude plugin / agent / command totals into this inventory. Upstream [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) is proof that the *job* exists, not a count this repo has earned.

| ID | Kind | Status | Source (Claude, for melt) | Notes |
|----|------|--------|---------------------------|-------|
| threat-model-lite | skill | melted | plugins/threat-modeling (STRIDE + boundaries) | Assets, actors, boundaries, STRIDE-as-questions, controls. No attack trees or exploit steps. |
| dependency-audit | skill | melted | plugins/supply-chain-security/skills/dependency-risk-assessment | Advisories, reachability, pins, adopt/reject. No CVE PoCs. No fake 0–10 composite. |
| secrets-scan | skill | melted | plugins/secrets-management/skills/secret-detection (+ hygiene loop) | Path + pattern type + REDACTED. Rotate + manager. No live key verification. |
| secure-defaults | skill | stub | plugins/security-hardening | Cookie/TLS/AuthN cue only. |
| access-review | skill | stub | plugins/identity-access-management | Role cue only. |
| incident-runbook | skill | stub | plugins/incident-response | Detect → contain cue only. |
| defensive-logging | skill | stub | plugins/siem-log-management | Log/redact cue only. |
| secops-orchestrator | agent | stub | suite coordinator | Calls melted + stub specialists; not a melted specialist. |

This repo now: **3 melted skills**, **4 stub skills**, **1 stub agent**.

Where they live: melted skills in `plugins/libre-secops-grok/skills/<name>/SKILL.md` (the plugin installs them); stubs in `stubs/<name>/SKILL.md` (nothing installs them); the agent in `AGENTS/secops-orchestrator.md`.

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match the canonical file above. CI checks it.

## Pack entries (installed, not melted)

The marketplace also lists every plugin of [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) as a remote entry: **33 entries**, all pinned to one pack commit (the `sha` in `.grok-plugin/marketplace.json`). Grok reads those plugin folders as they are. They are not counted in the melted inventory above. `scripts/pin-pack.sh` re-pins them; CI fails when the pack gains or loses a plugin.

Three of them (`penetration-testing`, `red-team-operations`, `bug-bounty-methodology`) are written for authorized offensive engagements. Their pack descriptions scope them to authorized assessments, programs and engagements. The defensive-only rule binds the melted skills in this repo.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
