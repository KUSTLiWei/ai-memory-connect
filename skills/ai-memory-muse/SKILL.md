---
name: ai-memory-muse
description: Set up or repair ai-memory for Muse desktop/cloud, selecting its native conversation exporter and own-model worker instead of Muse Code CLI hooks.
---

# Muse entry

This entry is for Muse desktop/cloud. Its conversation source is
`chat.read_messages`; it is not the separate Muse Code CLI product.
Inspect the local authorized service first and reuse it. If absent, load
[service installation](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-install/SKILL.md).

Load only the missing stage:

- MCP/CLI access and usage Skills: [agent setup](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-agent-setup/SKILL.md).
- Conversation ingestion: [Muse capture](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-muse-capture/SKILL.md).
  The Rust source converter lives in `crates/ai-memory-workstream/src/adapters/muse/`;
  the relay command supplies shared privacy, queue, delivery and checkpoints.
- Extraction model: [model setup](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-setup/SKILL.md).
  With only runtime-owned inference, use the local model bridge and worker.
- Pending inference on an already configured bridge: [model worker](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-worker/SKILL.md).

Verify native capture, own-model inference and Rust-produced knowledge separately.
The model bridge runs locally; GitHub transport follows the owner's separate
choice. Report whether capture/worker triggers actually run automatically, or
still require explicit invocation. Preserve the existing daily library during
isolated acceptance and keep worker conversations excluded from ingestion.
