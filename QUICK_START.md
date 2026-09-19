# Quick Start — LibreSecOps for Grok Build

> From zero to a defensive review in under 5 minutes.

## Prerequisites

- Grok Build installed and working
- A service or repo to harden (authorized / your own)

## Install skills (repo-local)

```bash
git clone https://github.com/HermeticOrmus/LibreSecOps-Grok-Build.git
cd your-project
mkdir -p .grok/skills
cp -R /path/to/LibreSecOps-Grok-Build/skills/* .grok/skills/
```

Or user-global:

```bash
mkdir -p ~/.grok/skills
cp -R /path/to/LibreSecOps-Grok-Build/skills/* ~/.grok/skills/
```

## First-run teach cue

1. **Model** — "Run threat-model-lite on this service: assets, actors, trust boundaries."
2. **Defaults** — "Run secure-defaults on auth, cookies, and TLS settings."
3. **Secrets** — "Run secrets-scan for smell patterns — do not print secret values."

## Hard rules

- Defensive guidance only.
- No exploit steps, payloads, or attack scripts.
- Never embed or echo real secrets.

## Smoke checklist

- [ ] Skills visible to Grok
- [ ] One threat model or secure-defaults review
- [ ] No secrets or exploit content in output
