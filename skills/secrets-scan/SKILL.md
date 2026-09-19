---
name: secrets-scan
description: Detect secret smells in repos and configs for Grok Build. Never print secret values.
---

# Secrets Scan

Find exposure patterns; redact values.

## Steps
1. Search for high-entropy / key-shaped patterns in git history and configs.
2. Report file paths and pattern types only — redact values.
3. Prefer secret managers; rotate if exposure suspected.
4. Add pre-commit / CI scanning guidance.
5. Never paste live credentials into chat or skills.
