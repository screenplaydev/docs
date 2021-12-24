# Syncing with remote

{% hint style="info" %}
Very often as you're building, the remote trunk branch will move ahead of your local repository, and you'll want to pull in the latest changes and resolve any conflicts before you land your pull requests.
{% endhint %}

## Syncing your repo

If your remote trunk branch (i.e. `origin/main`) gets ahead of your local repository while you're developing, you can use `gt repo sync` to bring your stack up-to-date.&#x20;

`gt repo sync` does 3 things:

1. Pulls in the latest changes from `origin/main` (or whatever your trunk branch is)
2. Prompts you to delete any stale local branches which have been merged in (this works even if you use squash-and-merge)
3. Recursively rebases your up-stack branches which have not been merged

If you want to automatically push any local branches which were rebased as a result of `gt repo sync`, you can pass the `-r` flag, i.e. `gt repo sync -r`.

## Resolving rebase conflicts

{% hint style="info" %}
Resolving rebase conflicts while running `gt repo sync` works just like it does for `gt commit create` or `gt commit amend`.
{% endhint %}

If `gt repo sync` encounters any conflicts as it recursively rebases your stacked branches, you'll be prompted to resolve your conflicts before continuing.  You can do this with the following workflow:

```bash
# find which files have conflicts
gt status

# * resolve the rebase conflicts *

# add your changes
gt add -A

# continue the rebase operation
gt continue
```

Now that you've resolved any conflicts, it's time to land your stack!
