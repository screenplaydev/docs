---
description: Some commonly asked questions about the CLI
---

# FAQ

### Why did my `submit` overwrite a coworker's changes to my branch?

We use `git push --force-with-lease` under the hood for our push, which _should_ ensure this doesn't happen.  You should only be able to overwrite changes that you have already pushed from your machine or synced to your machine with `downstack get`.

Using this option is just like using `--force` (i.e., push to a branch on remote even if remote's SHA cannot be fast-forwarded to the new SHA), with the caveat that if the remote's SHA for the branch doesn't match the "remote-tracking branch" on your machine (e.g. `refs/remotes/origin/feature`), it will fail, as this means that someone else has updated the branch since you last pushed to it or pulled it.  Graphite respects the "remote-tracking branch", only updating it on a `submit` or `downstack get` operation.

The main thing that can mess this up is if you have some other tooling (i.e. some VSCode extension) that is `git fetch`ing your branches in the background, which could update the "remote-tracking branch" and result in the `--force-with-lease` check passing even if someone has updated the branch to a commit that you haven't synced to your repo (or pushed yourself).



### Why does the Graphite CLI use branches instead of commits to represent atomic changes in a stack?  Shouldn't you use commits for this?

\
You are **definitely** not the first to ask! :stuck\_out\_tongue: We've thought about this a lot internally, especially with many of us having come from working with stacked changes in Phabricator and/or Mercurial.  There are plenty of other CLI tools that simulate the stacked changes workflow using commits locally.

Our classic answer is that branches are the unit of code review for pull requests in GitHub, and supporting stacked changes is ultimately all about making the code review experience, the true collaborative part of engineering, easier for everyone.  Maintaining compatibility with existing tooling is important for us.

As for why we allow more than one commit on each branch, once we decided on branches, we went with supporting multi-commit branches to provide our users with more options.  Some folks are used to creating standard git histories on their local branches, and like to retain that history if they don't squash-and-merge their PRs.

If you feel strongly that the single-commit workflow is better, there's a simple way to get it! Just don't use `gt commit create`, and if you end up with multiple commits on a branch by accident, you can always use `gt branch squash` to get your branch back to a single commit.  This way, you can essentially only use `gt`, and your workflow will look something like:\
\
(making use of lots of shortcuts and short-form flags)

```
# make changes to the codebase

gt bc -am "my first commit"

# make some more changes

gt bc -am "my second commit"

# now we're ready to submit!

gt ss -np

# got some feedback?

gt bco my_first_commit

# address comments
gt ca -an
gt ss

# ... etc

```

As you can see, replicating the classic workflow is possible, and if you do things like this, you should never really have to worry about the difference between a branch and a commit!



### Why are my actions running twice?

Because `stack submit` both performs a `git push` and a GitHub API call, occasionally GitHub will pick up both as a [`synchronize`](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#pull\_request) event on the PR.

We recommend using GitHub's [concurrency](https://docs.github.com/en/actions/using-jobs/using-concurrency) configuration to ensure that you do not have duplicated CI!
