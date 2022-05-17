# Collaborating on a stack

Version 0.18.4 introduces a new command, `gt downstack sync`, that allows you to pull your coworker's stacks from remote into your local repository.

For example, coworker A could create and submit their branch:

```
gt branch create my_branch -m "My changes"
gt ss
```

Then, coworker B could pull the branch to their machine:

```
gt downstack sync my_branch
```

This will sync all branches that `my_branch` depends on (starting from the bottom of the stack).  If any of the branches already exist locally, Graphite will prompt you to confirm that you'd like to overwrite your local copy, and abort if you change your mind.

\
Coming soon: Instead of overwriting local changes, rebase them onto the remote branch.

We are still iterating on this feature, and would love to hear more on how we can add tooling around it to better support your workflow in the [#downstack-sync-preview](https://graphite-community.slack.com/archives/C03DZLX3MHQ) channel on our [community Slack server](https://join.slack.com/t/graphite-community/shared\_invite/zt-v828g9dz-TIRvlutxTCqgZmxnsO9Knw)!

{% hint style="success" %}
`gt downstack sync` is also the recommended workflow for developers who work on more than one machine — submit draft PRs for your stack on one machine with `gt stack submit` and use then use `downstack sync` from the other device!
{% endhint %}

### Got coworkers that don't use Graphite yet?

We strongly recommend that coworkers who wish to collaborate on a branch both use `gt` to ensure that the dependencies are managed and synced correctly as you work together.

Only branches that your coworkers have submitted with `gt` can be synced down to your local, as we rely on the Graphite submission to keep track of the dependency tree.

If you want to stack on top of your non-Graphite-using coworkers’ branches, the current recommendation would be to use `git pull`  and set its dependency with `gt us onto <trunk>`, although this flow will change slightly in the near future.
