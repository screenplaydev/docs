# The Graphite workflow

{% hint style="info" %}
Now that you've set up your CLI & web dashboard, it's time to get familiar with the core Graphite development workflow.
{% endhint %}

Let’s say you’re starting work on a new feature (i.e. adding stories to Instagram), which involves API, server, and front-end changes…

![](<../.gitbook/assets/architecture diagram.png>)

Today, you’d probably create one large “stories” feature branch with changes across all 3 surfaces…

![](<../.gitbook/assets/00 big PR.png>)

…but with stacked changes, you can break up your changes into smaller branches which are easier to review:

![](<../.gitbook/assets/00 stacked prs.png>)

You would start by creating your first branch:

```bash
# check out your trunk branch
gt branch checkout main

# * build Stories API *

# create a new branch off of main with your changes and add a commit in a single line:
gt add -A # add all unstaged change (same syntax as git add)
gt branch create feat-stories-API -m "Stories - API [1/3]"

# alternatively, you could do this with a single line:
gt branch create -a feat-stories-API -m "Stories - API [1/3]"
```

{% hint style="info" %}
Note that if you don't pass in a branch name, `gt branch create` will auto-generate a branch name from your commit message.  You can configure a prefix for `gt branch create` to add to all of your auto-generated branch names using `gt user branch-prefix` - see the [**CLI command reference**](../guides/graphite-cli/cli-command-reference.md#user) for more details.
{% endhint %}

![](<../.gitbook/assets/01 new branch.png>)

Note that unlike a standard git workflow - where you create a new branch before working on your feature - with `gt` you do the following:

1. Start by building your feature on an existing branch
2. Add your unstaged changes with `gt add`
3. Create a new branch and commit simultaneously with `gt branch create -m "{your commit message}"`

Graphite keeps track of the parent branch so that it can always fix your stacks if something changes underneath.

```bash
# view your current stacks as tracked by Graphite
gt log # (log view)
gt log short # (compact view of just stacks)
```

![](<../.gitbook/assets/01a highlight meta.png>)

You can then submit your branch for review when you’re done the API portion…

```bash
# submit your current stack to GitHub, creating or updating PRs for each branch as necessary
gt stack submit

# view your currrent stacks
gt log
```

![](<../.gitbook/assets/02 put up PR.png>)

…and continue to work by creating more stacked changes as your first PR is being reviewed.

```bash
# * build Stories server *

# create a new branch off of feat-stories-api and add a commit
gt branch create -a feat-stories-server -m "Stories - server [2/3]"

# * build Stories frontend *

# create a new branch off of feat-stories-server and add a commit
gt branch create -a feat-stories-frontend -m "Stories - frontend [3/3]"

# view your currrent stacks
gt log
```

![](<../.gitbook/assets/04 stack branches.png>)

After your PR is approved, it can be merged in.

```bash
# * merge in your changes on GitHub or the Graphite web dashboard [coming soon] *
```

![](<../.gitbook/assets/05 first PR approved.png>)

Whenever you merge a PR into `remote/main`, you can sync Graphite to make sure the parent branch info for your local repo stays up to date with the remote repo…

```bash
# pull in the latest trunk branch from remote, delete local branches which were merged in, and recursively rebase upstack branches which have not been merged
gt repo sync

# view your current stacks
gt log
```

![](<../.gitbook/assets/06 merge first PR.png>)

…and then continue to work on your stacked changes without worrying about conflicts.

![](<../.gitbook/assets/07 updating meta.png>)

You can also submit multiple changes at a time for review and approval:

```bash
# navigate to the top of the stack
gt branch checkout main
gt branch next 2 # -> checks out the branch 2 levels upstack (in this case feat-stories-frontend)

# submit the current branch and all downstack branches to GitHub for review
gt stack submit

# view your current stacks
gt log
```

![](<../.gitbook/assets/08 stack approved (2).png>)

Whenever you push a stack of PRs to GitHub, Graphite automatically adds a comment to every PR in the stack to help your reviewers navigate between them:

![](<../.gitbook/assets/Screen Shot 2021-09-21 at 10.35.14 AM.png>)

Once all the PRs in your stack have been approved, you can merge them all into trunk (see [Landing a stack of branches](https://www.notion.so/Graphite-user-guide-66300dcb2d29453fb1d6ea013a8d4859) for more on this).

![](<../.gitbook/assets/09 merge stack.png>)

Graphite makes it easy to continue building without interruptions - just sync your repo, start working on your next feature, and then start a new stack by creating a branch.

```bash
# pull in the latest trunk branch from remote, delete local branches which were merged in, and recursively rebase upstack branches which have not been merged
gt repo sync
gt branch checkout main

# * work on update to stories *

# create a new branch off of feat-stories-server
gt branch create -a feat-stories-update -m "Stories - update"

# view your current stacks
gt log
```

![](<../.gitbook/assets/10 new branch.png>)

Now that you have a sense of how to build using the stacked changes workflow with Graphite, feel free to explore our detailed documentation and start creating stacks!
