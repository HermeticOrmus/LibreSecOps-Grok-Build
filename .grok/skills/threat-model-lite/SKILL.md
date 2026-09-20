---
name: threat-model-lite
description: Lightweight threat model for Grok Build. Defensive framing only — assets, actors, trust boundaries, mitigations.
---

# Threat Model Lite

Frame residual risk so the team can harden. Do not produce attack recipes.

Gold Hat: name the user jobs and the assets that serve them first, then teach one reusable control per finding. A model that only lists scary verbs extracts attention. A model that leaves a ranked control list empowers the next change.

**Defensive only.** No exploit steps, payloads, PoCs, attack trees, or "how an attacker would." Capabilities belong on actors; procedures do not.

## When to use

- A new service, feature, or integration is about to ship
- Auth, tenancy, payments, file intake, or a new trust boundary changed
- You need a short model for a design review — not a week of theater
- `secops-orchestrator` asked for assets and boundaries first

Do not use this skill as a pentest, red-team plan, or CVE reproduction. After the model, hand posture gaps to `secure-defaults` and `access-review` (still stubs). Hand supply-chain and credential hygiene to `dependency-audit` and `secrets-scan` (melted). Hand detect/respond leftovers to `defensive-logging` and `incident-runbook` (stubs). Call the stub; do not invent its depth.

## Operating steps

1. **Name jobs and assets.** Who is this for, what must they accomplish, what must stay confidential / integer / available? If you cannot name the job, ask. Guessing assets is extraction.
2. **Draw trust boundaries.** Client, edge, app, data, identity provider, third-party API, build → prod, operator → infra. Each crossing is in scope.
3. **List realistic actors and capabilities** (not steps). End user, stolen-session holder, neighboring tenant, insider with a role, supplier of a dependency, anonymous internet. Capability = what they can already do from their side of a boundary.
4. **Walk STRIDE as questions**, one element at a time. Record only findings you can point at (asset or flow + category + existing control or gap).
5. **Rank residual risk.** Critical → high → medium → low. Propose hardening controls the owners can actually ship. Teach one sentence.

Stop if the request is "show how to break this." Refuse. Offer the control list instead.

## STRIDE (defensive mnemonic)

Each letter is a **property to protect**, not a recipe.

| Category | Property | Ask | First controls |
|----------|----------|-----|----------------|
| Spoofing | Authentication | Can a principal be confused with another? | MFA, short-lived tokens, bind session to client where appropriate |
| Tampering | Integrity | Can data or code change without an authorized writer? | Validate input, signed/HMAC payloads, parameterized queries, immutability |
| Repudiation | Accountability | Can a sensitive action happen with no attributable log? | AuthN on the event, tamper-evident logs, trusted time |
| Information disclosure | Confidentiality | Can someone read data they should not? | TLS, encryption at rest, least privilege, data minimization, safe errors |
| Denial of service | Availability | Can load or a cheap request starve the job? | Rate limits, quotas, timeouts, backpressure |
| Elevation of privilege | Authorization | Can a role gain a capability it was not granted? | Fail-closed AuthZ, object-level checks, no client-trusted roles |

Walk **per element**, not as a brainstorm:

| Element | Usually ask |
|---------|-------------|
| External entity (user, vendor, IdP) | Spoofing |
| Process (app, worker, function) | All six |
| Data flow | Tampering, disclosure, availability |
| Data store | Tampering, repudiation, disclosure, availability |

## Trust boundaries to enumerate

- User → CDN / edge
- Edge → application
- Application → datastore
- Application → each external API
- Application → queue / bus
- Service A → service B
- Build pipeline → production
- Operator → infrastructure

If a flow does not cross a named boundary, say so. Do not invent a threat to fill a cell.

## Measurable checks

| Check | Pass | Fail |
|-------|------|------|
| Job named | Who / task / primary action in one line | "the system" with no user |
| Assets listed | Data classes + jobs they serve | Only product nouns ("the API") |
| Boundaries drawn | Every external call and store has a crossing | "internet vs us" as the only line |
| Actors have capabilities | "can call authenticated routes as tenant T" | "hacker exploits the stack" |
| Finding is specific | Element + STRIDE + control gap | Adjective-only ("insecure") |
| Control is a harden | Config, check, or rejection the team can ship | "monitor more" with no owner |
| No attack procedure | Residual risk + control | Steps, payloads, or PoC |

Severity (pick the higher if unsure, and say why):

| Rank | Meaning |
|------|---------|
| Critical | Unauthenticated or cross-tenant reach to a crown-jewel asset; no compensating control |
| High | Authenticated misuse of a privileged job, or secret/PII likely to leave a boundary |
| Medium | Missing control on a real boundary; blast radius is one tenant or one function |
| Low | Defense-in-depth debt; existing control already covers the job |

If you did not inspect the code or config, mark the finding **unverified** and say what to open. Do not invent a score out of 10.

## Worked example — Team Notes (authorized fiction)

Job: a signed-in member creates a private note. Primary action: save note. Crown jewels: note bodies, session tokens, tenant membership.

Boundaries: browser → TLS edge → notes API → Postgres; API → OIDC issuer.

Actors (capabilities only):

- Member: create/read own notes in tenant A
- Neighbor tenant: authenticated in tenant B only
- Anonymous internet: hit login and public health
- Dependency supplier: code that runs in the API process at next install
- Operator: deploy + DB console (break-glass)

Abridged model:

```markdown
## Job
Signed-in member saves a private note in their tenant.

## Assets
- Note body (confidential to tenant)
- Session / access token
- Tenant membership table

## Boundaries
browser —TLS→ API —IAM user→ Postgres; API → OIDC.

## Findings
1. **High — elevation / disclosure (unverified until AuthZ read).** Notes fetch is keyed by `note_id` only. Residual: a member in tenant A may read tenant B if IDs are guessable. Control: enforce `tenant_id = session.tenant_id` on every read/write; reject 404 on miss (do not leak existence across tenants if that is the product rule).
2. **Medium — spoofing.** Sessions have no recorded absolute lifetime in repo. Control: short TTL + rotation on privilege change; document the TTL you actually ship.
3. **Medium — repudiation.** No audit row for "note exported." Control: log actor, tenant, action, object id — never the note body (`defensive-logging`, stub).
4. **Low — availability.** Create has no recorded per-user quota. Control: per-principal rate limit on write.

## Fixes now
1. Object-level tenant check on note read/write.
2. Write down and enforce session TTL.
3. Audit export without bodies.

## Teach
A tenant id in the client is a claim, not a control — the store enforces membership.

## Leftovers
Cookie / TLS flags → `secure-defaults` (stub). Lockfile advisories → `dependency-audit`. `.env` smells → `secrets-scan`.
```

That is a threat model: jobs, boundaries, ranked gaps, controls. Not a walkthrough.

## Anti-patterns

- **Shelf-ware.** If it is not in the design note or the PR for the change, it will not be read. Keep this skill's output short enough to paste.
- **STRIDE with no mitigations.** Each kept finding gets a control or an explicit accept + owner + review date.
- **Every cell critical.** Rank. Engineering can ship a handful of controls per sitting.
- **Actors as movie villains.** "APT" without a capability is theater. "Anyone who can call this route with a stolen session" is usable.
- **One-time ceremony.** Re-run when a boundary or asset changes.
- **Offensive completion.** If a human asks for the exploit, stop. Residual risk + harden is the whole product.

## Output shape

```markdown
## Job
[who / task / primary action]

## Assets
- [data or capability] — [why it matters]

## Boundaries
[client] → [edge] → [app] → [store / vendor]

## Actors
- [role] — [capability on which side of which boundary]

## Findings (severity-ranked)
1. **[Critical|High|Medium|Low] — [STRIDE].** [element] [gap]
   Residual: [what remains if we do nothing]
   Control: [concrete harden]
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

Empty findings are allowed. Invented issues are not. Unverified is a first-class label.

## Quality bar

A pass is done when every finding names an element, a STRIDE category, a residual, and a control — and the document contains zero exploit steps. Refuse vibe-only notes ("it's probably fine", "make it zero-trust") unless you can turn them into a check.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](../../GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](../../README.md).
