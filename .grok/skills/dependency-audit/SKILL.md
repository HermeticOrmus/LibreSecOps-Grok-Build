---
name: dependency-audit
description: Dependency risk review for Grok Build projects. Advisory-focused, not exploit development.
---

# Dependency Audit

Reduce supply-chain risk you can actually prioritize. Advisories and maintenance facts beat folklore.

Gold Hat: teach *why this package is in the blast radius* while you rank it. A CVE dump that cannot be acted on extracts panic. A short, reachable, owned upgrade list empowers the next release.

**Defensive only.** Cite advisory IDs, affected versions, and upgrade targets. Do not include exploit PoCs, payloads, or reproduction steps for any CVE — including "just to verify."

## When to use

- Before adding a direct dependency
- After a lockfile change, Dependabot/Renovate PR, or incident rumor
- Periodic hygiene on an app you own or are authorized to review
- `secops-orchestrator` asked for supply-chain posture

This skill is melted. Pair with `secrets-scan` (melted) when a package manager token or `.npmrc` looks committed. Hand host/image hardening leftovers to `secure-defaults` (stub). Do not invent an SBOM factory this repo does not ship.

## Operating steps

1. **Inventory.** Direct deps from the manifest; notable transitives from the lockfile (auth, crypto, HTTP, template, parse). Name the ecosystem (npm, PyPI, crates, Go, Maven, gems).
2. **Facts, not vibes.** For each notable package: pinned version, last release you can see, known advisories (OSV / GitHub Advisory / NVD IDs only). If you did not query a database, mark **unverified**.
3. **Context.** Direct vs transitive, runtime vs dev/test, whether your code path can reach the reported function. Unreachable still gets a scheduled bump — it is not "ignore forever."
4. **Rank and plan.** One upgrade (or replace/remove) per finding the team can test. Prefer maintained packages; commit lockfiles; no `*` / `latest`.
5. **Teach one sentence.** Why this package, why this SLA.

Stop if asked for a working exploit against the advisory. Give the patched version and the test you will run after upgrade.

## Risk dimensions (no fake composite score)

Do not invent a 0–10 "risk score." Rank with the table below. Say which facts you have.

| Dimension | Look at | Pass signal |
|-----------|---------|-------------|
| Advisory | CVE / GHSA / OSV id, fixed version | Id + upgrade target named, or "none found (date queried)" |
| Exposure context | Direct? runtime? processes user input? | Dev-only linter ≠ prod auth library |
| Reachability | Do we call the reported area? | **reachable** / **likely** / **unknown** / **not in our tree** |
| Maintenance | Last release, bus factor, security response | Commit or release in the last year, or a written replace plan |
| Pinning | Lockfile committed; manifest not `*` / `latest` | Lockfile in git; CI fails if missing |
| Provenance | Typosquat lookalikes; unexpected install scripts | Name matches intent; no unexplained `postinstall` |

License conflict (copyleft in a proprietary ship, missing license) is a finding. It is not a CVE. Say **legal**, not **critical vuln**.

## Triage (authorized apps you maintain)

| Advisory class | Reachable in prod? | First action |
|----------------|--------------------|--------------|
| Known exploited (CISA KEV) or actively abused, runtime | Yes or unknown | Patch or isolate now; do not wait for a bundle of unrelated bumps |
| High/critical advisory, runtime | Yes | Patch in the current change window; add a regression check |
| High/critical, runtime | No / transitive unused | Schedule; still pin the fixed version when cheap |
| Medium | Any | Next regular release or 90 days, whichever is sooner |
| Low / informational | Any | Opportunistic; do not page people |
| No advisory, unmaintained (>12 months) | Runtime | Replace or vendor-with-eyes; do not "hope" |

If EPSS or KEV is cited, name the source and date. If you did not look them up, do not imply you did.

## New dependency (before it lands)

```markdown
## Adopt? [name]

- Job it serves:
- Stdlib or existing dep instead?
- License:
- Last release (date):
- Open advisories (ids or none):
- Transitive count (order of magnitude):
- Install scripts / native binaries: [none / justified]
- Decision: ADOPT / DEFER / REJECT
```

Reject lookalikes of popular names, packages whose only "docs" are a readme with a badge, and anything that demands `*` or `latest`.

## Measurable checks

| Check | Pass | Fail |
|-------|------|------|
| Lockfile | Committed and used in CI install | "Just use npm install" with no lock |
| Pins | Manifest ranges are intentional; no `*` / `latest` | Floating prod deps |
| Advisory list | Ids + fixed versions, or explicit none | "there are CVEs" with no ids |
| Order | Runtime reachable first | Alphabetical dump of 200 transitives |
| Upgrade is testable | One change + how you will know it worked | "bump everything" |
| No PoC | Upgrade + test | Curl/payload/repro of the CVE |

## Worked example — notes API lockfile (authorized fiction)

Ecosystem: npm. Direct runtime: `express`, `pg`, `jsonwebtoken`. Lockfile present.

```markdown
## Inventory
- express@4.18.2 (direct, runtime, HTTP)
- jsonwebtoken@8.5.1 (direct, runtime, tokens)
- pg@8.11.3 (direct, runtime, datastore)
- Notable transitive: `semver` (via jwt stack) — verify in lockfile

## Findings
1. **High — advisory (example id, unverified against live OSV at review time).** `jsonwebtoken` 8.x has published GHSA upgrades to 9.x for algorithm/verification bugs. Reachable: **yes** (we verify tokens). Control: upgrade to the patched 9.x line; run existing auth tests; do not paste a forged-token recipe.
2. **Medium — maintenance.** `left-pad`-shaped tiny util (if present) with no release in 18 months. Control: remove or replace with stdlib.
3. **Low — pinning.** Dev dep on a linter at `latest`. Control: pin; leave runtime pins as-is.

## Fixes now
1. Bump `jsonwebtoken` to the patched range; lockfile commit; auth test suite.
2. Pin the linter.
3. Record "no KEV cited" and the query date.

## Teach
A lockfile is the bill of materials you can actually rebuild — the manifest is a wish.

## Leftovers
Image/OS packages → `secure-defaults` (stub). CI secret for npm → `secrets-scan`.
```

Cite real IDs from a real query when you run this on a real repo. The versions above are teaching furniture, not a live advisory claim.

## Anti-patterns

- **CVE theater.** Pasting a scanner PDF without reachability or an owner.
- **Equal panic.** Unreachable transitive ≠ prod auth library.
- **Mass bump.** One runtime change, test, then the next.
- **Unpinned prod.** `latest` is not a strategy.
- **Exploit to "confirm."** Confirmation is: patched version installed + tests green + advisory marked resolved.
- **Fake precision.** No homemade 6.7/10 composite. Severity ranks are enough.

## Output shape

```markdown
## Ecosystem
[npm | PyPI | …] — lockfile [present/missing]

## Inventory
- [name@version] — [direct/transitive] [runtime/dev] [job]

## Findings (severity-ranked)
1. **[Critical|High|Medium|Low] — [advisory|maintenance|pinning|legal].**
   Id: [GHSA/CVE/OSV or none]
   Reachable: [yes|likely|unknown|no]
   Control: [upgrade / remove / replace / accept+date]
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

## Quality bar

A pass names packages, versions, and next actions. It never contains a reproduction. If the scanner is unavailable, say **unverified** and still fix pinning and unmaintained direct deps you can see.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](../../GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](../../README.md).
