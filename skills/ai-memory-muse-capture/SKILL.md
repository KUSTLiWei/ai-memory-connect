---
name: ai-memory-muse-capture
description: Capture approved Muse cloud conversations incrementally through chat.read_messages and the Rust relay, preserving source roles and stable message sequence.
---

# Capture Muse conversations

This is Muse desktop/cloud, not Muse Code CLI. Use the host's formal
`chat.read_messages` tool. Read only the explicitly selected chat(s); bind each
to the intended owner and workspace/project. Exclude model-worker chats.

Use `companions/ai-memory-relay/README.md` from the
[pinned runtime](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-connect/references/runtime.md)
for the native export envelope and executable commands. Reuse an existing queue;
new queues use producer `ai-memory.knowledge` and wire identity `muse-cloud`.
Before exporting text, run capture-policy preflight as described there; denied
or metadata-only capture must not export full text.

1. Read `muse-cursor` for this chat's saved sequence.
2. Call `chat.read_messages` newest first, at most 20 turns per page. Save raw
   responses and the exact cursor used, following `next_cursor` until reaching
   the saved sequence or `has_more=false`. Keep exports private.
3. Run `capture-muse` on the complete bounded export, then `flush`. Rust checks
   pagination, roles, timestamps and stable IDs, queues events durably, and
   advances the checkpoint. Inspect delivery outcomes; acknowledged drops are
   not stored memories. Retry unchanged exports after failures.
4. If extraction was requested, run the configured local pipeline. Host-agent
   inference uses the separately installed
   [model worker](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-worker/SKILL.md).

This tool exports user/assistant text, not complete tool trajectories. Preserve
that limit. An unfinished turn is not a session-end event. Do not reconstruct
messages from summaries or invent timestamps/sequence IDs.

Muse has polling hooks/cron, but no formal task-end Skill hook. For authorized
automatic capture, configure a bounded host trigger on these named chats and
verify it runs after new messages; retain the same queue across VM restarts.
If no trigger is configured, say capture is on-demand. If history exceeds the
adapter's limits, stop and arrange a bounded migration; never jump the checkpoint
past unseen pages. Other hosts reuse the relay envelope with their own source
adapter rather than pretending their transcript is Muse's format.
