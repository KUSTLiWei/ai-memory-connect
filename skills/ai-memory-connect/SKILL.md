---
name: ai-memory-connect
description: Connect an agent to the user's ai-memory knowledge service. Use when onboarding a new agent or computer, installing ai-memory, or checking whether agents on one machine can share an existing service. Reuse an authorized installation before creating one.
---

# Connect to ai-memory

Run this on the computer that executes the agent's tools. The result is a working
memory connection and discoverable usage Skills. The user should only need to
provide this repository URL. Determine paths, platform and agent integration
yourself; ask only for missing authorization or an unresolved choice of service.

## 1. Find an existing service first

Inspect this agent's memory configuration, project `.ai-memory.toml`, available
`ai-memory` executable, configured data directory, and local service manager.
Do not print credentials. Probe the configured endpoint and make an authenticated
`memory_status` call; a listening port or HTTP 200 alone is insufficient.

- Same machine and same authorized owner: reuse the endpoint and data directory.
  Each agent gets its own integration and task scope, not a second server or DB.
- An installed but stopped service: recover that installation before creating one.
- HTTP 401/403: resolve authorization; do not create an empty replacement.
- An unreachable configured remote: report the failure and determine whether
  independent local storage was requested. Do not silently split the knowledge base.
- Multiple owners or installations: identify the intended one before connecting.

Check compatibility through the actual tool schemas and required endpoints.
Do not upgrade a shared server silently: identify affected agents, back up its
data, and obtain approval when the current request does not cover that upgrade.
Never use `serve --force` to bypass another server's lock.

## 2. Install only when no suitable service exists

Read [the source pin](references/runtime.md) for the exact code repository and revision.
Use that revision's documentation and CLI `--help`; do not install upstream
`latest` and assume it contains this fork's personal-knowledge features.

The code repository is private. First try this machine's existing authorized
GitHub access. If it is missing or insufficient, ask the user to complete GitHub
login on this machine, then resume. If a token is needed, have the user enter it
through the local credential tool; never ask them to paste it into this Skill,
repository, or chat. Store credentials in the host credential manager or an
owner-only credential file, never in a remote URL. Do not publish private code
or change repository visibility to bypass authorization.

Inspect OS/architecture, persistent storage, available memory and process manager.
Keep checkout, configuration and knowledge under persistent user storage, not
`/tmp`. SQLite is bundled: no separate database server is needed.

Clone the code into an unused persistent directory, check out the pinned commit,
and build with the toolchain from `rust-toolchain.toml`:

```sh
cargo build --locked --release -p ai-memory-cli -j 1
```

Install the resulting binary in a user-owned location without overwriting another
installation. If Rust/build dependencies are missing, use their official install
instructions. If memory or permissions block the build, report that concrete
blocker; do not repeatedly retry or fall back to a different feature version.

For a supported harness and working per-user service manager, preview then apply:

```sh
ai-memory --data-dir "$MEMORY_DATA_DIR" setup --agent <actual-harness> --plan
ai-memory --data-dir "$MEMORY_DATA_DIR" setup --agent <actual-harness> --yes
```

Set `MEMORY_DATA_DIR` to the persistent directory chosen above. Replace the
placeholder with the harness identified from `setup --help`. For an existing
service managed elsewhere, use `--no-service` and its actual configuration.
Name only the requesting harness; do not automatically reconfigure other agents.

If the platform has no usable user service manager, use its documented persistent
process facility to run:

```sh
ai-memory --data-dir "$MEMORY_DATA_DIR" init
ai-memory --data-dir "$MEMORY_DATA_DIR" serve --transport http --bind 127.0.0.1:49374 --enable-api
```

Choose a different port only after resolving any existing listener. Keep one
server per data directory, local authentication, and owner-only credential files.
`ai-memory server` manages endpoint profiles; it does not launch a server.
Record restart ownership. A background shell process alone does not prove restart
or VM-replacement persistence. Do not expose a public port for local agents.

## 3. Wire this agent and install usage Skills

Use the native installer when it supports the actual product. Otherwise use the
pinned source's `docs/programmatic-memory.md` for Streamable HTTP `/mcp`, or its
CLI through the agent's execution tool. Check JSON-RPC errors and `result.isError`.
Do not invent an unsupported client configuration.

Install the canonical usage Skills with `install-skills --target-dir <skill-root>`
and the routing snippet with `install-instructions --compact --target <rules-file>
--skills-target-dir <skill-root>`. First identify the host's real discovery roots
and rules file. Preserve unrelated instructions and unmanaged same-named Skills.
Copy this repository's `skills/ai-memory-connect` directory into that discovery
root too, including its `references/` directory. Confirm discovery.

Muse desktop/cloud is not automatically the `setup --agent muse` integration,
which targets Muse Code CLI. On Muse, inspect its own installed documentation for
custom Skills, tool execution and persistent processes, then use those facilities.
Do not operate a different computer to install on Muse's behalf.

For each task, send explicit workspace/project and current domain, device, tools
and capabilities where supported. Coding and non-coding agents share knowledge;
task context chooses what is relevant. Role defaults are not access permissions.

## 4. Connect learning and automatic knowledge sync

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

The public Skill, private program code and private knowledge are separate repositories.
Code-repository access never implies permission to read personal knowledge. Check
GitHub authorization separately for each repository; use repository-scoped grants
where available. Background sync must never target the program-code repository.
Resolve the knowledge repository during setup:
- If the user already has one, reuse that repository and clone its existing branch
  before exporting local knowledge. Keep existing directories and scope mappings.
- If none exists, create a dedicated **private** knowledge repository in the user's
  chosen account under the installation authorization. If that authorization or
  account choice is missing, ask for it; an inaccessible repository is not absent.
- Never create a new knowledge repository just because this machine has no clone.

For cross-machine sharing, use the user's explicitly selected private knowledge
repository and scopes with `companions/ai-memory-wikisync/README.md`. Build that
companion separately if needed. Sync Markdown knowledge, evidence and portable
Skills; never sync live SQLite, authentication files or machine login state.
Do not import repository test fixtures as real personal knowledge.

Automatic knowledge sync is part of onboarding. Once the owner has selected the
private knowledge repository and scopes and completed GitHub authorization, build
the wikisync companion and configure one persistent worker per checkout using
`repository ... --apply --watch 3600 --max-pending-files 100`. Either one hour since
the last successful exchange or 100 changed files triggers Git exchange; both are
configurable. The Rust worker polls every 30 seconds, fetches remote updates even
when local knowledge is unchanged, and retains failed pushes across restarts.
Each Git exchange must fetch and merge the remote before pushing. The worker first
checkpoints local allowed changes in a local commit, then fetches/merges, imports
merged knowledge, and pushes. That local checkpoint is not an upload. A conflict
stops the push; preserve both sides and ask for resolution. Authentication failure
requires login, not a replacement repository or force push.
Use the host's actual persistent process manager and protected credential storage.
Verify it comes back after process restart and exchanges a harmless scoped test
change. Do not claim a detached shell process survives VM replacement.

Only knowledge is automatically committed and pushed. Program-code changes remain
manual. Never infer the private knowledge destination from the code remote. If the
knowledge repository or authorized scopes are missing, ask the user for those and
report sync as pending setup. Retain Git conflicts for resolution, without force
pushes or automatic selection of one side.

## 5. Verify and hand back

Use an isolated, explicitly labeled onboarding-test project. Write a harmless test
page, query and read it through the agent's actual interface, correct it with a
version precondition, then confirm the latest result. Test both a coding and a
non-coding task context without writing synthetic personal preferences globally.
If learning is configured, verify source input → extraction → recall → correction
using actual calls and evidence. Test restart recovery only for the new service
you installed, not a shared service other agents are using.

Report: reused/new installation, code commit, endpoint, data path, actual read/write
results, capture/learning status, restart behavior, Git sync status and any blocker.
Never equate “installed,” “discoverable,” “invoked” and “verified.” Stop when the
onboarding is complete or a concrete user-only authorization blocks the next step.
