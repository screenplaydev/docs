# Mixing gt and git

{% hint style="info" %}
Under the hood, `gt` uses native `git` commands and stores all of the metadata on your stacks in the `.git` folder in your repo. We intend `gt` to entirely replace `git` in your workflow, but if you ever need to do something we don't support natively, you can always jump back to `git` and then sync your changes with Graphite.
{% endhint %}

## Git passthrough

Graphite's CLI features a **git passthrough** - `gt` will pass any unrecognized commands thru to `git`, so you can run commands like `gt status` or `gt remote`, even though they aren't native commands in `gt`.

{% hint style="info" %}
Git passthrough helps to avoid confusion about when to use `gt` vs. `git` - you can (and should) use `gt` for everything! For commands like `gt branch` which differ from their git equivalents, we recommend using the `gt` version to automatically keep your stacks in sync.
{% endhint %}

## Fixing your stacks when you use `git`

Because of the "restacking" model, it is always safe to change your branches with `git` commands, as a `gt upstack restack` once you are done will ensure that their children are correctly rebased on top.

You can even perform complex actions like an interactive rebase and then `upstack restack`, although we do provide a convenience command `gt branch edit` that combines these two operations into a single command.

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

There is also a `gt branch untrack` command that you can use to stop tracking a branch with Graphite without deleting it.
