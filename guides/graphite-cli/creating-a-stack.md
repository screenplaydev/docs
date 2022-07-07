# Creating a stack

{% hint style="info" %}
Graphite's CLI makes it easy to stack dependent branches on top of each other.
{% endhint %}

### Creating your first branch

{% hint style="warning" %}
Note that unlike a standard git workflow - where you create a new branch before working on your feature - with `gt` we recommend the following:

1. Start by building your feature on an existing branch
2. Stage your changes (`gt add -A`)
3. Create a new branch with those changes (`gt branch create`)

This follows the traditional "stacked changes" workflow of treating each branch as an atomic changeset that contains (at least to start with) a single commit. If you prefer to start with an empty branch, we do support that as well — see the next section.
{% endhint %}

The below snippet shows two equivalent ways to create a branch with a single commit on it using `gt branch create`.

```bash
gt branch checkout main

# * build feature part 1 *

# create a new branch off of main with your changes and add a commit
gt add -A # add all unstaged change (same syntax as git add)
gt branch create -m "part 1" # -> creates a commit with message "part 1" on a branch named "05-04-part_1" (inferred from the date and your commit message) 

# alternatively, you can combine the last 2 commands into a single line:
gt branch create -a -m "part 1"
```

{% hint style="info" %}
Because you didn't pass in a branch name in the above example, `gt branch create` auto-generated a branch name from your commit message. You can configure a prefix for `gt branch create` to add to all of your auto-generated branch names using `gt user branch-prefix` — see the [**CLI command reference** ](command-reference-v0.19.5.md)for more details.
{% endhint %}

### Creating a branch without staged changes

Graphite also supports creating your branch before starting to code! In order for Graphite's branch metadata to correctly track dependencies, Graphite will create an empty commit if you create a branch without staged changes, which you are free to either amend or commit on top of with the [**commit-level commands**](updating-a-mid-stack-branch.md). If you prefer not to amend commits, you can avoid an empty commit in your history with squash-and-merge.

### Stack more branches on top

Once you have created a branch with your first set of changes, you can continue to build your stack by issuing more `gt branch create` commands as you work!

```bash
# * build feature part 2 *

# create a new branch on your stack
gt branch create -a -m "part 2"

# * build feature part 3 *

# create another new branch on your stack
gt branch create -a -m "part 3"
```

Now that you've created a stack, you can use Graphite's CLI to easily visualize it in your terminal.
