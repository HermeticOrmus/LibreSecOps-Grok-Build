# libre-secops-grok

The Grok-native LibreSecOps plugin. It carries the skills melted for Grok Build, and only those. Defensive only: no exploit steps, payloads, or attack PoCs, and no secret value is ever printed.

| Skill | Job | Melted from (pack plugin) |
|-------|-----|---------------------------|
| `threat-model-lite` | Assets, actors, trust boundaries, STRIDE as questions, ranked controls | `threat-modeling` |
| `dependency-audit` | Advisories, reachability, pins, adopt or reject | `supply-chain-security` |
| `secrets-scan` | Path and pattern type, `REDACTED` values, rotate and prevent | `secrets-management` |

Install:

```bash
grok plugin marketplace add HermeticOrmus/LibreSecOps-Grok-Build
grok plugin install libre-secops-grok@libre-secops-grok --trust
```

The four stub skills are not in this plugin. They live in [stubs/](../../stubs/), and each names the pack plugin that holds the real depth. The same marketplace installs those pack plugins.

Manifest: [.grok-plugin/plugin.json](./.grok-plugin/plugin.json). Honest inventory: [docs/DEPTH_MATRIX.md](../../docs/DEPTH_MATRIX.md). The v0 bundle stub this plugin replaces is kept at [stubs/libresecops-core/](../../stubs/libresecops-core/).
