# Collaborating on a stack

`gt downstack get` allows you to pull your coworker's stacks from remote into your local repository.

For example, coworker A could create and submit their branch:

```
gt branch create my_branch -m "My changes"
gt ss
```

Then, coworker B could pull the branch to their machine:

```
gt downstack get my_branch
```

This will sync all branches that `my_branch` depends on (starting from the bottom of the stack).  If any of the branches already exist locally and differ from the remote version, Graphite will ask to either overwrite your local changes, or rebase them on top of the remote version.

{% hint style="success" %}
`gt downstack get` is also the recommended workflow for developers who work on more than one machine — submit draft PRs for your stack on one machine with `gt stack submit` and use then use `downstack get` from the other device!
{% endhint %}

### Got coworkers that don't use Graphite yet?

We strongly recommend that coworkers who wish to collaborate on a branch both use `gt` to ensure that the dependencies are managed and synced correctly as you work together.

Only branches that your coworkers have submitted with `gt` can be synced down to your local, as we rely on the Graphite submission to keep track of the dependency tree.

If you want to stack on top of your non-Graphite-using coworkers’ branches, the best way to do this is `git pull`  and  `gt branch track`.

### Submitting branches in collaborative stacks

Generally, `submit` prefers that your branches are restacked, but **only the branches that you are submitting need to be restacked**.  This means that if you are working on some branches stacked on top of an old version of a coworkers branch, and you'd prefer not to mess with their changes, including rebasing them, you can use `gt upstack restack` on your own changes and `gt upstack submit` to submit them without restacking (and therefore changing) your coworker's branch.  Once your coworker lands their changes, you can `repo sync` and restack your branches on the new version of `main`!
