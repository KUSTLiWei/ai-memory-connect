---
name: ai-memory-knowledge-sync
description: Pull or push the private personal knowledge repository, configure automatic sync, or diagnose its failures. Does not update program-code repositories.
---

# Sync personal knowledge

First distinguish the requested operation: one exchange, inspect status, or
install/change the background worker. Reuse existing configuration. For a one-time
exchange, use its same `repository` arguments with `--apply` and without `--watch`;
avoid racing the existing worker and retain its configuration. A status-only request
reads status/logs and does not initiate a push. No installation guide is needed
when the service and companion already work.

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

Use the existing worker's endpoint, checkout, branch, mappings and family allowlist.
For new setup, select those from the user's intended knowledge scopes; do not infer
authorization from a directory name. Prefer installed `ai-memory-wikisync --help`.
Read only the repository-mode section of `companions/ai-memory-wikisync/README.md`
if more detail is needed; no source checkout is needed for an existing working binary.
If the companion is actually missing, read [installation](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-install/SKILL.md)
for that component only. If GitHub access fails, read [authorization](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-github-auth/SKILL.md). Sync Markdown knowledge, evidence and portable
Skills; never sync live SQLite, authentication files or machine login state.
Do not import repository test fixtures as real personal knowledge.

Automatic knowledge sync is part of onboarding. Once the owner has selected the
private knowledge repository and scopes and completed GitHub authorization, use
the available wikisync companion and configure one persistent worker per checkout using
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

Keep the original task scope: routine push/pull does not reinstall a worker, wire
another agent or configure extraction. Include evidence scopes required by selected
knowledge. Add a newly authorized project's mapping when onboarding that project;
static mappings do not discover new projects automatically.

Done when the intended local/remote knowledge agrees, or a specific conflict/auth
failure is reported with local work retained. For background setup, additionally
verify the worker is running and resumes after its own restart. Read only the sync
section of [verification](https://github.com/KUSTLiWei/ai-memory-connect/blob/main/skills/ai-memory-verify/SKILL.md) if needed.
