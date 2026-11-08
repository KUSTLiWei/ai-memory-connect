---
name: ai-memory-connect
description: Route ai-memory installation, agent connection, GitHub authorization, knowledge-repository sync, or setup verification to one task-specific skill. Start here when given this repository link.
---

# Choose the agent, then the missing step

For onboarding or agent-specific capture/connection repair, identify the actual
host first: [Codex](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-codex/SKILL.md)
or [Muse desktop/cloud](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-muse/SKILL.md).
Read only that entry. Other agents use agent setup to check their actual native
integration or external event contract; do not guess another product's adapter.
For a clearly named shared task such as knowledge sync or model configuration,
use the matching row below directly.

Identify the requested result and inspect only the relevant existing configuration.
Keep the original task when following a dependency; return to it after the missing
piece is resolved. Reuse completed setup rather than restarting onboarding.

| Task or observed gap | Read only this Skill |
|---|---|
| Install a missing program, recover a stopped service, or assess an incompatible version | [Service installation](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-install/SKILL.md) |
| GitHub access to the specific private repository is missing or rejected | [GitHub authorization](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-github-auth/SKILL.md) |
| Connect a new agent, install usage Skills, configure its memory tools | [Agent setup](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-agent-setup/SKILL.md) |
| Configure/change the extraction model | [Model setup](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-setup/SKILL.md) |
| Capture Muse cloud conversations | [Muse capture](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-muse-capture/SKILL.md) |
| Process pending host-agent inference requests | [Model worker](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-worker/SKILL.md) |
| Pull/push knowledge, configure its repository or background sync, inspect sync failure | [Knowledge sync](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-knowledge-sync/SKILL.md) |
| Verify a changed connection, learning path or sync worker | [Verification](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-verify/SKILL.md) |

Read the selected file from an installed copy or fetch that file from the link.
Do not clone/read the entire Skill repository or load every child Skill. Fetch a
reference only when the selected step calls for it. Child Skills can be invoked
directly when the task is already clear.

For **new onboarding**, inspect the configured service first: authenticated
`memory_status` must succeed. A listening port alone is insufficient. Reuse the
same authorized owner's working service; restore a stopped installation before
creating one. A 401 is an authorization gap, not an absent service. Resolve an
unreachable configured remote or multiple installations before creating storage.
Then load only the missing stage: installation, agent setup, knowledge sync, and
relevant verification. Read each stage when reached, not all at the beginning.

For **routine knowledge sync**, start with knowledge sync. If it works, stop;
installation and model setup do not belong in that task. Ordinary memory queries
and writes use the runtime's installed retrieval/durable-page Skills instead of
this deployment flow. If “update the repository” is ambiguous, identify whether
it means program code or personal knowledge before writing.

Report the actual result and remaining blocker. This router does not authorize
new access, service upgrades or unrelated configuration changes.
