# adwa-skills

Tobia's skill registry, served by GitHub Pages: https://messaynew-cyber.github.io/adwa-skills/

## What is here

| Path | Purpose |
|---|---|
| `index.json` | The catalog the app reads (`skill_store action=available`). |
| `<name>.skill` | A JSON manifest: schema, name, description, parameters, code, version, requires_keys, sha256, changelog. |
| `index.html` | The browsable registry page. |

## Publishing

From Tobia:

```
skill_store action=annotate tool="<name>" version="2.0.0" changelog="what changed"
skill_store action=publish   tool="<name>"
```

`publish` uploads the manifest and regenerates `index.json` through the GitHub Contents API.
It refuses to upload anything whose code contains a credential (`hf_`, `ghp_`, `AIza`, `sk-`, `AKIA`, `xox`).

Pages serves the new version about a minute after the commit.

## Manifest schema 2

```json
{
  "schema": 2,
  "name": "example",
  "description": "What it does",
  "parameters": { "prompt": { "type": "string", "description": "..." } },
  "code": "import os\n...",
  "author": "tobia",
  "version": "1.0.0",
  "requires_keys": ["HUGGINGFACE_TOKEN"],
  "changelog": "",
  "homepage": "",
  "sha256": "<hash of code>",
  "exported_at": 0
}
```

## Install

```
skill_store action=install name="example"
```

Install checks the content type, refuses a version that is not newer than the installed one
(`force=true` overrides), and verifies required keys are configured before registering.
