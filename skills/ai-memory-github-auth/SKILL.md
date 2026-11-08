---
name: ai-memory-github-auth
description: Resolve missing or rejected GitHub access for a specified private ai-memory code or knowledge repository. Use existing authorization first.
---

# Authorize the requested repository

Identify the exact repository and required read/write operation. Code access does
not grant personal-knowledge access. Try this machine's existing GitHub login,
SSH identity or credential helper without printing credentials.

If access is missing or rejected, ask the user to complete GitHub login on this
machine. If a token is required, have the user enter it through the local credential
tool; keep it in the credential manager or an owner-only credential file. Never
put it in chat, a Skill, a Git remote URL, or a committed file. Use repository-scoped
grants where available; do not copy another computer's login or change visibility.

An inaccessible repository is not an absent repository: do not create a replacement.
Validate access to the exact repository after login. Read access alone does not
prove write access; verify a push only as part of the user's authorized sync task.

Done when the required access is established, or the user must complete login.
Return to the interrupted step; do not start installation or sync independently.
