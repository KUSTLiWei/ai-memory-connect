---
name: ai-memory-install
description: Install or recover a missing ai-memory service or binary; assess required upgrades. Use only when service discovery identifies an installation gap.
---

# Install or recover the service

Work on the machine executing this agent's tools. Reuse a suitable service owned
by the same authorized user. Inspect its executable, data directory, endpoint and
process manager; recover a stopped service before making another. Check required
tool schemas/endpoints for compatibility. Before upgrading a shared service,
identify affected agents and back up data; obtain approval if the task does not
cover the upgrade. Never bypass the single-instance lock with `serve --force`.

Only for a needed download/build, read [the pinned runtime source](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-connect/references/runtime.md).
Use that commit's CLI and documentation. If private source access is missing,
read [GitHub authorization](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-github-auth/SKILL.md) and resume here after login.
Install only the missing component: if the memory server works and only wikisync
is absent, build `companions/ai-memory-wikisync/Cargo.toml` with `cargo build
--manifest-path companions/ai-memory-wikisync/Cargo.toml --locked --release -j 1`.
Do not rebuild/reconfigure the server for that case.

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

Muse desktop/cloud differs from Muse Code CLI (`setup --agent muse`). Use Muse's
own documented process facility; do not operate another machine on its behalf.

Done when the required binary works and, for a server installation, authenticated
status succeeds. Return the endpoint, data path, commit and restart behavior to
the calling step. Wire the agent only when that is part of the original task.
