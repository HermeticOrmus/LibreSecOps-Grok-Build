# Stubs

A stub is a thin cue: a name, a one-line job, and five steps. It is a reminder, not a playbook, so nothing here installs. Each stub names the pack plugin that holds the real depth, and that plugin installs from this repo's marketplace.

| Stub | Job | Real depth (pack plugin) | Install |
|------|-----|--------------------------|---------|
| [secure-defaults](./secure-defaults/SKILL.md) | Secure-by-default review cue | [`security-hardening`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/security-hardening) | `grok plugin install security-hardening@libre-secops-grok --trust` |
| [access-review](./access-review/SKILL.md) | AuthZ and least-privilege cue | [`identity-access-management`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/identity-access-management) | `grok plugin install identity-access-management@libre-secops-grok --trust` |
| [incident-runbook](./incident-runbook/SKILL.md) | Detect, contain, recover cue | [`incident-response`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/incident-response) | `grok plugin install incident-response@libre-secops-grok --trust` |
| [defensive-logging](./defensive-logging/SKILL.md) | Log and redact cue | [`siem-log-management`](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code/tree/main/plugins/siem-log-management) | `grok plugin install siem-log-management@libre-secops-grok --trust` |

Also here: [libresecops-core/](./libresecops-core/), the v0 plugin bundle stub. It had no manifest and installed only a copy of the stub orchestrator. It is kept as the record; [plugins/libre-secops-grok](../plugins/libre-secops-grok/) replaces it.

The suite agent [AGENTS/secops-orchestrator.md](../AGENTS/secops-orchestrator.md) is also a stub coordinator. It stays where [AGENTS.md](../AGENTS.md) points, and nothing installs it: you merge it by hand.

## Melt a stub

1. Write the skill to the melted bar in [docs/DEPTH_MATRIX.md](../docs/DEPTH_MATRIX.md) and [docs/MELT_RULES.md](../docs/MELT_RULES.md): when to use, steps, measurable checks, a worked example, an output shape. Defensive only: no exploit steps, payloads, or PoCs, and no secret values.
2. `git mv stubs/<name> plugins/libre-secops-grok/skills/<name>`, drop the stub line, and give the frontmatter a routing description (`Use when ...`).
3. Copy it to `.grok/skills/<name>/SKILL.md` (CI checks the copy matches).
4. Update [docs/DEPTH_MATRIX.md](../docs/DEPTH_MATRIX.md), this table, and the README skills table.

The dogfood copies of these stubs in `.grok/skills/` match the files here, so a session opened in this repo sees them described as stubs.
