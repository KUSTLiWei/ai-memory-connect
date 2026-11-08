---
name: ai-memory-verify
description: Verify the specific ai-memory connection, extraction path or knowledge synchronization just changed. Report observed results and untested boundaries.
---

# Verify only the changed path

Select the section matching the task. Routine sync does not require model tests;
read-only status checks do not authorize test writes. Use existing evidence where
it already proves the requested outcome.

## Agent connection

Call authenticated status through the agent's actual interface. For authorized
onboarding tests, use a labeled isolated project: write a harmless page, query/read
it, correct it with a version precondition, and confirm the latest result. Check
JSON-RPC errors and `result.isError`, not just HTTP 200. For full onboarding, test
coding and non-coding task contexts without creating global synthetic preferences.

## Capture or learning

If this path changed and the provider is authorized, exercise actual source input
→ extraction → recall → correction. Confirm source attribution and the resulting
page/version. Without model authorization, report extraction unavailable; deliberate
reads/writes may still work. Do not substitute another model without authorization.

## Knowledge synchronization

Confirm the intended repository/branch, retained local changes, and successful
remote push. After a pull, confirm applicable remote changes reach the local memory
interface. Check that credentials, live SQLite and runtime state are not tracked.
For a new/changed background worker, inspect success time and pending state, restart
only that worker when safe, and verify it resumes from the same checkpoint. Do not
restart a shared memory server for this test. A running shell process does not prove
VM-replacement or machine-reboot recovery. Report those separately if untested.

Report only relevant evidence: actual endpoint/commit, read/write or extraction
result, Git commit and worker status, plus blockers. Installed, discoverable,
invoked and verified are different states. Stop when the requested check is complete.
