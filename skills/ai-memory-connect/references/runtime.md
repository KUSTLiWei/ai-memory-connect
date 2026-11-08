# Runtime source

- Code: https://github.com/KUSTLiWei/ai-memory
- Branch: `feat/personal-coding-memory`
- Commit: `5a420f95c3d943fe551080e216feea75d7066621`
- Access: private repository; use this machine's existing authorized GitHub access.

Use the exact commit above. If access is unavailable, install this public Skill,
ask the user to log in to GitHub on this machine, and resume after access succeeds.
Accept any required token only through the local credential tool. Do not copy
another machine's credentials, change repository visibility, or substitute an
upstream release. The public Skill alone does not grant access to private code.

Clone the code into an unused persistent directory with an authorized HTTPS or
SSH remote, fetch the named branch, and check out the pinned commit. Confirm
`git rev-parse HEAD` before building. No Linux binary for this revision is bundled
here; source builds use the repository's pinned Rust toolchain.

From the checked-out code, consult `docs/install.md`,
`docs/programmatic-memory.md`, `docs/external-lifecycle.md`,
`docs/cross-project-profile.md`, and `companions/ai-memory-wikisync/README.md`
only as the corresponding installation step needs them.

Knowledge storage is chosen separately by the owner. This public repository
never supplies a private knowledge URL, token, or preauthorized model account.
