# Mixing gt and git

{% hint style="info" %}
Under the hood, `gt` uses native `git` commands and stores all of the metadata on your stacks in the `.git` folder in your repo.  We intend `gt` to entirely replace `git` in your workflow, but if you ever need to do something more advanced, you can always jump back to `git` and then sync your changes with Graphite.
{% endhint %}

## Git passthrough

Graphite's CLI features a **git passthrough** - `gt` will pass any unrecognized commands thru to `git`, so you can run commands like `gt status` or `gt remote`, even though they aren't native commands in `gt`.

{% hint style="info" %}
Git passthrough helps to avoid confusion about when to use `gt` vs. `git` - you can (and should) use `gt` for everything! For commands like `gt branch` which differ from their git equivalents, we recommend using the `gt` version to automatically keep your stacks in sync.
{% endhint %}

## Fixing your stacks when you use `git`

If you end up using `git` instead of `gt` to create a branch or commit and want to make sure it's properly tracked in Graphite, you can do the following to make sure your stacks are up-to-date:

```bash
# update your local repo to account for branches or commits created outside of Graphite
gt stack fix --rebase

# abbreviated, this is:
gt sf --rebase
```

{% hint style="info" %}
`gt stack fix --rebase` will automatically update PRs and commits created outside of `gt` to reflect **Graphite's record of your stacks** - i.e. if you create a new branch or commit mid-stack and then run `gt stack fix --rebase`, Graphite will rebase the upstack changes to prevent your stack from forking.
{% endhint %}

## Regenerating your stacks from `git`

If you're a power user who wants to update your local repo using `git` and then rebuild Graphite's record of your stacks based on the dependencies of your git branches, you can run the following command:

```bash
# update Graphite's record of your stacks to match your git repo
gt stack fix --regen
```

{% hint style="info" %}
`gt stack fix --regen` will update Graphite's record of your stacks to reflect **branch dependencies in your git repo** - i.e. if you create a new branch or commit mid-stack and then run `gt stack fix --rebase`, Graphite's record of your stacks will now show that you've intentionally added a fork in your stack.
{% endhint %}
