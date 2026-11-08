---
name: ai-memory-model-setup
description: Configure this deployment's extraction model, including API or CLI providers and Muse's agent-owned model bridge. Use for model setup or changes, not routine memory retrieval.
---

# Connect this deployment's model

Inspect the existing service configuration and the host's authorized model access.
Reuse an API/CLI provider when available; the private runtime's
`docs/llm-providers.md` is authoritative for provider/model/base URL/auth settings.
Credentials belong to this machine. GitHub authorization and model authorization
are separate. Keep the current working deployment model unless a change is requested.

When the host exposes inference only inside agent tasks (verified for Muse cloud),
use `companions/ai-memory-agent-bridge/README.md` from the [pinned runtime](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-connect/references/runtime.md).
Build its Rust companion locally. Initialize a private token file, configure
`openai-compat` against its loopback port, and let the service launcher load the
file as `LLM_API_KEY` without displaying or committing it. The worker CLI reads
that same file itself. Record the routing label and the actual host model when
available; a routing label is not proof of a specific vendor model.

Keep system evolution disabled unless separately requested. If already enabled,
check extraction overrides; an empty override inherits `llm_model`. The design
model must be supported by this deployment before any design work is enabled.
Preserve existing data, authentication, scopes and unrelated settings. Back up
changed configuration for rollback and restart only the requested local instance.

Install only the [model worker](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-model-worker/SKILL.md)
when the host-agent bridge is selected. A host polling/cron trigger must actually
wake that worker; a running bridge alone provides no automatic inference. Use a
separate worker chat excluded from capture. Report missing trigger support.

Verify a schema-constrained request through the selected provider, then ingest
fictional evidence into an isolated scope and run `ai-memory profile process`.
For a host-agent model, run the process in the background while the worker handles
its requests. Inspect the final report and resulting knowledge/evidence pages.
A successful claim/submit is transport evidence only. Do not replace the pipeline
with manual `memory_write_page` calls when testing automatic extraction.
