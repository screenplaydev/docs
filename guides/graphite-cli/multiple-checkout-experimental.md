# Multiple checkout (experimental)

_CLI v0.18.7 adds experimental support for linked worktrees. For context on worktrees, which allow you to manage multiple copies of your local working tree, see:_ [_https://git-scm.com/docs/git-worktree_](https://git-scm.com/docs/git-worktree)_._

{% hint style="info" %}
Previously, `gt` was not able to understand that it was in a linked worktree, and as such only supported hooking into the main `git` worktree for your local repository. Now, `gt` commands should largely work as expected in linked worktrees.
{% endhint %}

{% hint style="warning" %}
However, there is one big gotcha: one of the main limitations of multiple worktrees is that `git` will fail to check out a branch in one worktree if it is already checked out in another. Since the Graphite CLI relies heavily on rebasing, and rebasing requires checking out the branch to be rebased, you will need to be careful with the branches you have checked out in your other worktrees.
{% endhint %}

{% hint style="success" %}
We recommend only using one worktree for each stack off your trunk branch to limit confusing errors.
{% endhint %}
