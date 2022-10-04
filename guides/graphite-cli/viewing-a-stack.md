# Viewing a stack

{% hint style="info" %}
Graphite gives you 3 different ways to visualize your current stack.
{% endhint %}

Let's continue the example from the previous page and see what our current stack looks like!

### `gt log` (most common)

![](<../../.gitbook/assets/image (7).png>)

### `gt log short` (compact view)

![](<../../.gitbook/assets/image (20).png>)

### `gt log long` (detailed view)

![](<../../.gitbook/assets/image (1).png>)

{% hint style="info" %}
Note that `gt log long` is quite different from `gt log short` and `gt log` — it shows the `git` source of truth, i.e. the current git history, instead of Graphite's view of the world.  If you don't understand what this means yet, that's OK! We'll get into it in a little bit.
{% endhint %}

In fact, `gt log long` is just an alias for:

`git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)' --branches`

But we like the way it looks!

### Options for `log` and `log short`

`log` and `log short` both support the following options.  Since `log long` is just a shortcut for a git command it doesn't have any customizability in Graphite at the moment.

`gt log --stack` — only shows the direct descendants and ancestors of the current PR.  By default the commands show all branches currently tracked with Graphite.

`gt log --steps <n>` — implies `--stack` but only shows n levels of descendants and ancestors.

`gt log --reverse` — displays the log with trunk (e.g. main) at the top instead of the bottom.  Useful when you have larger stacks to keep their tips near the bottom of the output.

### Other details about your branches

Once you've submitted your branches with Graphite (we'll get to this later!), `gt log` also includes a link to the PR page and some details about its status.

You can also view some information for one branch at a time with `gt branch info` which by default shows, in addition to the PR info, the children and parents of the branch as well as the commit descriptions for each commit in the branch.  There are also `--desription` and `--patch` options to see the PR description (if one exists) and the changesets of each commmit.

_Now that you know how to visualize your stack, you can use Graphite to navigate it and submit your PRs!_
