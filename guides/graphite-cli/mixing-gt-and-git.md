# Mixing gt and git

{% hint style="info" %}
Under the hood, `gt` uses native `git` commands and stores all of the metadata on your stacks in the `.git` folder in your repo. We intend `gt` to entirely replace `git` in your workflow, but if you ever need to do something we don't support natively, you can always jump back to `git` and then sync your changes with Graphite.
{% endhint %}

## Git passthrough

Graphite's CLI features a **git passthrough** - `gt` will pass any unrecognized commands thru to `git`, so you can run commands like `gt add`or `gt status`, even though they aren't native commands in `gt`.

{% hint style="info" %}
Git passthrough helps to avoid confusion about when to use `gt` vs. `git` - you can (and should) use `gt` for everything! For commands like `gt branch` which differ from their git equivalents, we recommend using the `gt` version.
{% endhint %}

#### Git commands that Graphite users may find useful:

* `git add`: Stage files to be committed; `-p` is helpful for precise cases.
* `git stash`: Save changes for later (retrieve with `git stash pop`).  Since restacking requires the working tree to be clean, stashing changes you don't intend to commit is often necessary while using `gt`. The `-p` option is just like `git add`'s.
* `git diff`: See what has changed between two branches.
* `git status`: Keep track of your worktree and staging area, just like `git`
* `git rebase`: Useful for preparing branches created outside of Graphite to be tracked (see below).  Also potentially dangerous (see further below).

## Fixing your stacks when you use `git`

Because of the "restacking" model, it is always safe to update your branches with _simple_ `git` commands as a `gt upstack restack` on each child will rebase descendants such that they have the new version in their history.  We specify _simple_ here because there is some nuance to using `git rebase` — see below for details.

### Tracking branches created outside of Graphite

If you use `git` instead of `gt` to create a branch, you need to let `gt` know what its parent is.  That's what `gt branch track` is for.  When run, it prompts you to select a parent for the current branch from the branch's Git history. &#x20;

```bash
# Ensure the branch you want to track has the desired parent in its history
# In this case, we want to stack our branch `feature` on `main`
git checkout feature
git rebase main feature

# Now, we'll track our branch
gt branch track

# If there is more than one potential parent for feature,
# you will be prompted to select one.

# Now `feature` is tracked and `main` is its parent
gt branch down # checks out main

```

`gt branch track --force` skips the prompt and chooses the nearest ancestor that is already tracked.  See the command `--help` for more options.

{% hint style="info" %}
`gt branch track` can also be used to fix Graphite metadata if it ever becomes corrupted or invalid due to a Graphite bug or other issue.
{% endhint %}

### Tracking a whole stack at once

What if you've created a stack of multiple branches outside of Graphite?  `gt downstack track` allows you to track multiple branches recursively.  Run it from the tip of a stack to track the entire thing by selecting the parent of each branch until you reach a branch that is already tracked. The `--force` flag  chooses the nearest ancestor of each branch as its parent.

### Untracking a branch

There is also a `gt branch untrack` command that you can use to stop tracking a branch without deleting it from `git`.  **Note that this will also result in all descendants of this branch becoming untracked as well**; to avoid this, use `upstack onto` to move them onto a new parent first (learn more about `upstack onto` [here](https://docs.graphite.dev/guides/graphite-cli/modifying-a-stack#gt-upstack-onto)).

### On using `git rebase`

The CLI's engine works keeps track of the base of each branch — i.e. the commit in its history that corresponds to its parent branch.  This means that if you use a vanilla `git rebase` that removes that commit from the branch's history, your branch and its children may suddenly become untracked! In order to bring the branch back into Graphite, you will need to ensure the branch is correctly based on its parent, and then use `gt track` to fix its metadata.

Rebases that don't remove that base of the branch from its history are safe — for example, running a `git rebase -i` on the commits of a branch is safe, although we provide a convenience command for this called `gt branch edit` that runs an interactive rebase followed by `upstack restack` on each child of the branch.



