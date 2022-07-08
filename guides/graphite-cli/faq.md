---
description: Some commonly asked questions about the CLI
---

# FAQ

### Why did my `submit` overwrite a coworker's changes to my branch?

We use `git push --force-with-lease` for our push, which _should_ ensure this doesn't happen.

Details:\
Using this option is just like using `--force` (i.e., push to a branch on remote even if remote's SHA cannot be fast-forwarded to the new SHA), with the caveat that if the remote's SHA for the branch doesn't match the "remote-tracking branch" on your machine (e.g. `refs/remotes/origin/feature`), it will fail, as this means that someone else has updated the branch since you last pushed to it or pulled it.  Graphite respects the "remote-tracking branch", only updating it on a `submit` or `downstack get` operation.

The main thing that can mess this up is if you have some other tooling (i.e. some VSCode extension) that is `git fetch`ing your branches in the background, which could update the "remote-tracking branch" and result in the `--force-with-lease` check passing even if someone has updated the branch to a commit that you haven't synced to your repo (or pushed yourself).
