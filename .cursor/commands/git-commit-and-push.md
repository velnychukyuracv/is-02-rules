---
description: "Stage all changes, commit with a message, and push to remote"
---

Run the following git commands in sequence:

1. `git add .` — stage all new and modified files
2. `git commit -m "$ARGUMENTS"` — commit with the provided message
3. `git push` — push to the remote branch

Before running:

- Confirm no `.env*`, keys, or credentials are being staged (`git status`)
- Ensure tests pass if code was changed (`yarn test:typecheck && yarn test`)
