# Syncing & resolving conflicts

{% hint style="info" %}
Very often as you're building, the remote trunk branch will move ahead of your local repository, and you'll want to pull in the latest changes and resolve any conflicts before you land your pull requests.
{% endhint %}

## Syncing your repo

If your remote trunk branch (i.e. `origin/main`) gets ahead of your local repository while you're developing, you can use `gt repo sync` to bring your stack up-to-date.&#x20;

`gt repo sync` does 3 things:

1. Pulls in the latest changes from `origin/main` (or whatever your trunk branch is)
2. Prompts you to delete any stale local branches which have been merged in
3. Recursively rebases your up-stack branches which have not been merged

## Resolving conflicts

{% hint style="warning" %}
We're actively working on improving the experience of resolving merge conflicts with `gt` - expect a significantly improved workflow here soon.
{% endhint %}

If `gt repo sync` encounters any conflicts as it recursively rebases your stacked branches, you'll be prompted to resolve your conflicts before continuing.  You can do this with the following workflow:

```bash
# find which files have conflicts
gt status

# * resolve the conflicts *

# commit your changes
gt commit create -a -m "your commit message"

# re-submit your stack to GitHub
gt stack submit
```

Again, `gt commit create` will handle all of the recursive rebases needed to bring your stack up-to-date.

Now that you've resolved any conflicts, it's time to land your stack!
