# Syncing with remote repository

{% hint style="info" %}
Often, as you're building, the remote trunk branch will move ahead of your local repository, and you'll want to pull in the latest changes and resolve any conflicts before you land your pull requests.
{% endhint %}

## Syncing your repo

If your remote trunk branch (i.e. `origin/main`) gets ahead of your local repository while you're developing, you can use `gt repo sync` to bring your stack up-to-date.

`gt repo sync` does a few things:

1. Pulls in the latest changes from `origin/main` (or whatever your trunk branch is)
2. Prompts you to delete any stale local branches which have been merged in (this works even if you use squash-and-merge)
3. Optionally restacks your up-stack branches which have not been merged and your current stack onto `main`. If you encounter any merge conflicts, you'll be prompted to resolve them as part of the restack — see the section on restacking for more details!

Let's say that we've squash-and-merged in one branch of our three-branch stack from earlier.  We can sync that change in from remote:

![](<../../.gitbook/assets/image (15).png>)

Now, if we run `gt log`, we see that `part_2` is based on `main`:

<img src="../../.gitbook/assets/image (6).png" alt="" data-size="original">

Since we didn't restack as part of the `sync` command here (we could have done so with `--restack`), we see that `part_2` needs a restack onto `main`.  We'll talk about what that means in the next section: [Restacking branches](https://docs.graphite.dev/guides/graphite-cli/restacking-branches).
