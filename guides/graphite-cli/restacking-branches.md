# Restacking branches

A key benefit of using Graphite as opposed to vanilla Git when working with stacks is dependency management for your branches, i.e. keeping track of the "parent" of a given branch.  When a parent branch changes in some way or is deleted, vanilla Git, because it does not have this concept of branch dependencies, leaves the parent as is.

The Graphite CLI introduces "restacking", which is the process of ensuring that the history of a branch is updated when its parent changes.  Consider where we left off on the [previous page](https://docs.graphite.dev/guides/graphite-cli/syncing-and-resolving-conflicts) after running `gt repo sync`.  Although `part_2` is now dependent on main, we haven't yet restacked it, and we can see that by viewing the Git history with `gt log long`:

![log long output](<../../.gitbook/assets/image (16).png>)

We see that `main` has advanced to the squash-and-merge commit for `part_1`, but `part_2`, even though it is supposed to be based on `main` now, is actually still sitting on the old version of `part_1`.  We can fix that with `gt upstack restack`.  This command, for the current branch and all recursive descendants, ensures that they are based on the current version of their parents.

![The results of restacking](<../../.gitbook/assets/image (19).png>)

After running our `restack` command, we can see that Git and Graphite are in agreement about the history.  Now, we might want to resubmit the restacked versions of these branches (`gt stack submit`), or maybe make some changes to them first to address review comments (see the following page).

{% hint style="info" %}
Restacking is running a `git rebase` under the hood, and as with any rebase, you may run into conflicts, in this case between the branch you are restacking and the new version of the parent.  Just like with git, you will be prompted to resolve conflicts before continuing, which you can do with `gt continue`, which is described in a little more detail in the next section.
{% endhint %}

Just like `submit`, there are `upstack`, `stack`, `downstack`, and `branch` restack commands.  It is likely that most of the time, `stack restack` and `upstack restack` will be the main commands that you use — `downstack restack` and `branch restack` are included for completeness.
