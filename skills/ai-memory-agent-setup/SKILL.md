---
name: ai-memory-agent-setup
description: Connect an agent to an existing ai-memory service and configure its usage Skills, lifecycle capture or model extraction when requested.
---

# Connect this agent

Use an authenticated working endpoint for the same authorized owner. If the
service is missing, return to [installation](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-install/SKILL.md); an auth
error is not a reason to create another service. Change only the requested part.
Use locally available runtime help/docs first; fetch only the named guide if absent.

## Agent connection and usage Skills

Use the native installer when it supports the actual product. Otherwise use the
pinned source's `docs/programmatic-memory.md` for Streamable HTTP `/mcp`, or its
CLI through the agent's execution tool. Check JSON-RPC errors and `result.isError`.
Do not invent an unsupported client configuration.

Install the canonical usage Skills with `install-skills --target-dir <skill-root>`
and the routing snippet with `install-instructions --compact --target <rules-file>
--skills-target-dir <skill-root>`. First identify the host's real discovery roots
and rules file. Preserve unrelated instructions and unmanaged same-named Skills.
Install this repository's short `ai-memory-connect` router if needed. Fetch child
Skills only when selected; do not concatenate their bodies into the rules file.

Muse desktop/cloud is not automatically the `setup --agent muse` integration,
which targets Muse Code CLI. On Muse, inspect its own installed documentation for
custom Skills, tool execution and persistent processes, then use those facilities.
Do not operate a different computer to install on Muse's behalf.

For each task, send explicit workspace/project and current domain, device, tools
and capabilities where supported. Coding and non-coding agents share knowledge;
task context chooses what is relevant. Role defaults are not access permissions.

## Capture and extraction — only when requested or missing during onboarding

Keep native lifecycle capture as the single source when available. Otherwise
follow `docs/external-lifecycle.md`: user dialogue, documents, tool output and
agent reports keep their real source and stable event identity. Never relabel
agent conclusions as user statements or install two capture paths for one event.

For contextual learning, configure `[profile] context_on_demand = true` and the
user's authorized extraction provider according to `docs/cross-project-profile.md`.
Authenticate on this machine; do not copy another computer's login. Check the
provider with `llm-test`, then exercise incremental `/admin/profile/process`.
Without a provider, deliberate memory reads/writes can work; report automatic
extraction as unavailable rather than claiming the whole learning loop works.

Done when this agent can call the intended memory interface and the requested
capture/extraction path is exercised. Model login is separate from GitHub login.
Use only the relevant section of [verification](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-verify/SKILL.md).
