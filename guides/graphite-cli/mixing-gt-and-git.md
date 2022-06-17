# Mixing gt and git

{% hint style="info" %}
Under the hood, `gt` uses native `git` commands and stores all of the metadata on your stacks in the `.git` folder in your repo. We intend `gt` to entirely replace `git` in your workflow, but if you ever need to do something we don't support natively, you can always jump back to `git` and then sync your changes with Graphite.
{% endhint %}

## Git passthrough

Graphite's CLI features a **git passthrough** - `gt` will pass any unrecognized commands thru to `git`, so you can run commands like `gt status` or `gt remote`, even though they aren't native commands in `gt`.

{% hint style="info" %}
Git passthrough helps to avoid confusion about when to use `gt` vs. `git` - you can (and should) use `gt` for everything! For commands like `gt branch` which differ from their git equivalents, we recommend using the `gt` version.
{% endhint %}

## Fixing your stacks when you use `git`

Because of the "restacking" model, it is always safe to update your branches with _simple_ `git` commands as a `gt upstack restack` on each child will rebase descendants such that they have the new version in their history.  We specify _simple_ here because there is some nuance to using `git rebase` — see below for details.

### Branches created outside of Graphite

If you end up using `git` instead of `gt` to create a branch or commit and want to stack on top of it with Graphite, you can use `gt track` to initialize its Graphite metadata:

```bash
# Ensure the branch you want to track has the desired parent in its history
# In this case, we want to stack our branch `feature` on `main`
git checkout feature
git rebase main feature

# Now, we'll check out `main` and track our branch
gt branch checkout main
gt branch track feature

# Now we're on `feature`, it is tracked, and `main` is its parent
```

{% hint style="info" %}
`gt branch track` can also be used to fix Graphite metadata if it ever becomes corrupted or invalid due to a Graphite bug or other issue.
{% endhint %}

### Untracking a branch

There is also a `gt branch untrack` command that you can use to stop tracking a branch with Graphite without deleting it.  Note that this will also result in all descendants of this branch becoming untracked as well; use `upstack onto` (next page) to move them onto a new parent first.

### On using `git rebase`

The CLI's engine works keeps track of the base of each branch — i.e. the commit in its history that corresponds to its parent branch.  This means that if you use a vanilla `git rebase` that removes that commit from the branch's history, your branch and its children may suddenly become untracked! In order to bring the branch back into Graphite, you will need to ensure the branch is correctly based on its parent, and then use `gt track` to fix its metadata.

Rebases that don't remove that base of the branch from its history are safe — for example, running a `git rebase -i` on the commits of a branch is safe, although we provide a convenience command for this called `gt branch edit` that runs an interactive rebase followed by `upstack restack` on each child of the branch.



