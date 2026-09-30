# libresecops-core (Grok plugin stub)

v0 record, superseded in v1.0.0. This folder had no manifest, so `grok plugin install` took it as an unversioned plugin holding only a copy of the stub orchestrator. The melted skills now ship as [plugins/libre-secops-grok](../../plugins/libre-secops-grok/). The text below describes the v0 layout.

Bundles core libresecops skills for install-from-path.

v0.1: skill bodies live under repo `skills/` (canonical) and `.grok/skills/` (dogfood). Melted: `threat-model-lite`, `dependency-audit`, `secrets-scan`. Copy or symlink into this plugin's `skills/` when packaging.

This plugin folder is still a stub bundle — packaging is not melted.
