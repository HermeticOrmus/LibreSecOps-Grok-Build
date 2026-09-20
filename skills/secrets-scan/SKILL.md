---
name: secrets-scan
description: Detect secret smells in repos and configs for Grok Build. Never print secret values.
---

# Secrets Scan

Find exposure patterns. Redact values. Move live material to a manager and rotate if exposure is plausible.

Gold Hat: teach the *hygiene loop* (detect → redact report → store elsewhere → rotate → prevent) while you scan. A dump of live keys extracts. A path + pattern-type + rotation owner empowers.

**Defensive only. Never print, echo, commit, or paste secret values — including "just the last four" if the value is short. Never write a harness that calls a vendor API to "see if the key works."**

## When to use

- First look at a repo you own or are authorized to review
- After a leak scare, a `.env` PR, or a "it works on my machine" config drop
- Before publishing a template or skill (this suite included)
- `secops-orchestrator` asked for credential hygiene

Melted. Pair with `dependency-audit` (melted) for registry tokens in lockfiles or CI. Hand session-cookie flags to `secure-defaults` (stub) and role blast radius to `access-review` (stub). This is not a vault product comparison and not a pentest of someone else's org.

## Operating steps

1. **Scope.** Working tree + (if authorized) git history. Note ecosystems: `.env*`, CI yaml, IaC, Docker, Kubernetes manifests, client bundles.
2. **Smell, do not exfiltrate.** Search for pattern *types* and assignment *names*. Record **path, line or commit, pattern type**. Replace any captured value with `REDACTED`.
3. **Classify.** Live-looking vs obvious fixture (`EXAMPLE`, `changeme`, `xxxxx`). When unsure, treat as live and say **uncertain**.
4. **Hygiene.** Prefer a secret manager or platform identity (OIDC, instance role) over long-lived static keys. If exposure is plausible (committed, logged, chatted), **rotate** the credential at the issuer — do not only delete the file.
5. **Prevent.** Pre-commit + CI scan; block on known prefixes; scan history (`fetch-depth: 0` or equivalent). Teach one sentence.

If a value appears in the tool output, overwrite it in your reply. If you cannot redact confidently, stop and say so.

## Smell types (report the type, never the value)

| Type | Shape you may name | Report as |
|------|--------------------|-----------|
| Cloud access key id | Vendor prefix + fixed length (e.g. AWS `AKIA…`) | `cloud-access-key-id` |
| Cloud secret / session | High-entropy assignment next to `SECRET`, `SESSION_TOKEN` | `cloud-secret` (redact) |
| Git forge PAT | `ghp_`, `github_pat_`, `gho_`, `ghs_`, `glpat-` | `forge-pat` |
| Chat / billing tokens | Vendor prefixes (`xoxb-`, `sk_live_`, `SG.`, `AIza`) | `vendor-token` + vendor name |
| Private key PEM | `BEGIN` + `PRIVATE KEY` | `private-key-pem` |
| Connection string | `scheme://user:pass@host` | `url-with-password` |
| Generic assignment | `password`, `secret`, `token`, `api_key` = `…` | `named-secret` |
| Client-side leak | Secret in a browser bundle or public repo example | `client-exposed` |

Do not paste a full regex catalog into chat. Do not include sample values that could be mistaken for live keys. Teaching tokens must be obviously fake (`AKIAEXAMPLE`, `ghp_REDACTED`, `-----BEGIN PRIVATE KEY-----\\nREDACTED`).

**History:** `git rm` does not unpublish a commit. If it was pushed, rotate, then purge or tombstone per the host's docs. Do not publish the old value in the ticket.

## Measurable checks

| Check | Pass | Fail |
|-------|------|------|
| Redaction | Output has `REDACTED` / type names only | Any live-looking value in the reply |
| Location | Path + line or commit SHA | "somewhere in the repo" |
| Classification | live / fixture / uncertain | Everything called "a leak" |
| Manager | Named store or platform identity | "put it in Slack and `.env`" as the plan |
| Rotation | Issuer + owner if exposure is plausible | Delete file only |
| Prevention | Hook or CI job named | "be careful" |
| No verification abuse | No "try the key against the API" | Live credential test |

Severity:

| Rank | Meaning |
|------|---------|
| Critical | Private key, prod DB URL, or cloud/forge token in a pushed commit |
| High | Same smells in the working tree, unpushed but shared; or secrets in CI logs |
| Medium | Fixture that looks live; `.env` without a gitignore; manager unused |
| Low | Example docs that still teach a bad pattern; scan not in CI yet |

## Hygiene loop (the actual product)

1. **Detect** — path + type.
2. **Contain report** — redact; limit who sees the finding.
3. **Move** — secret manager or workload identity; env at runtime from the platform, not from git.
4. **Rotate** — issuer UI/API; invalidate the old version; deploy the new reference.
5. **Prevent** — gitignore, pre-commit, CI, history scan; no secrets in skill examples.

Environments (dev / staging / prod) get **different** credentials. A leaked dev key must not open prod.

## Worked example — committed dotenv (authorized fiction)

Tree contains `app/.env` and `README.md` with a "sample" export.

```markdown
## Scope
Working tree + last 50 commits (authorized). Paths: `app/.env`, `README.md`.

## Findings
1. **Critical — named-secret / url-with-password.** `app/.env:12` — `DATABASE_URL` with embedded password. Value: REDACTED. Pushed in `abc1234`.
   Control: rotate the DB password at the host; load URL from the platform secret store; remove file from tree; treat history as still containing it until rotated.
2. **High — forge-pat.** `README.md:40` — text matching `ghp_` prefix in a "copy this" block. Value: REDACTED.
   Control: revoke the PAT at the forge; replace the block with `${GITHUB_TOKEN}` + a manager note.
3. **Medium — prevention.** No pre-commit or CI secret scan. Control: add a scanner that fails the build on known prefixes; `fetch-depth: 0` on that job.

## Fixes now
1. Rotate DB + forge credentials (owners: platform + repo admin).
2. Delete `app/.env` from the index; keep `.env.example` with empty placeholders only.
3. Add ignore + CI scan.

## Teach
Deleting the file without rotating leaves the old value valid in every clone that already fetched it.

## Leftovers
Who can read the manager → `access-review` (stub). App session cookies → `secure-defaults` (stub).
```

Notice: no values, no "curl -H Authorization" check.

## Anti-patterns

- **Printing to prove you found it.** Path + type is proof enough.
- **HEAD-only scans.** History is the usual graveyard.
- **Allowlisting whole `tests/` trees.** Fixtures sometimes contain a copied prod value. Allowlist *patterns* (`EXAMPLE`, `fake`, `placeholder`), not entire directories, unless you have reviewed them.
- **Pre-commit as the only gate.** `--no-verify` exists. CI is the enforcement layer.
- **One key for every environment.**
- **Verification against the vendor.** That is using the secret. Rotate instead.
- **Chat as a vault.** If it was pasted here, rotate.

## Output shape

```markdown
## Scope
[tree / history depth] — [authorized]

## Findings (severity-ranked)
1. **[Critical|High|Medium|Low] — [pattern type].** [path:line or commit]
   Value: REDACTED
   Control: [move + rotate + prevent]
2. …

## Fixes now
1. …
2. …
3. …

## Teach
[one reusable sentence]

## Leftovers
- [skill] — [what you did not pretend to finish]
```

If nothing smells, say so. Empty findings are allowed. Do not invent a key to look thorough.

## Quality bar

A pass redacts, locates, and names the next hygiene step. A fail is any secret value in the output, or a procedure to use a found credential.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](../../GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](../../README.md).
