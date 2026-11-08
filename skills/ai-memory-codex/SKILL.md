---
name: ai-memory-codex
description: Set up or repair ai-memory for Codex using its native hooks, transcript adapter and local model authorization.
---

# Codex entry

Identify the actual Codex CLI/desktop installation and its existing ai-memory
endpoint. Reuse an authenticated service for this owner. If absent, load only
[service installation](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-install/SKILL.md).

Use the runtime's supported Codex installer and native lifecycle hooks; inspect
local CLI help for the installed version. The native transcript parser lives in
`crates/ai-memory-workstream/src/adapters/codex/`, with shared transcript discovery
and cursors around it. Keep one capture owner; do not add the Muse exporter or a
second relay capture path to an already functioning Codex hook installation.

For MCP and usage Skills, load [agent setup](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-agent-setup/SKILL.md).
For missing or changed extraction, load [model setup](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-setup/SKILL.md).
Use this machine's authorized provider/model; Codex host identity alone does not
force a particular extraction model. Knowledge Git sync is a separate task.

Verify a real Codex lifecycle observation and a relevant query with explicit
scope when the client is static. Preserve working config and unrelated rules.
