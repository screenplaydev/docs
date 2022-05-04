# Creating a stack

{% hint style="info" %}
Graphite's CLI makes it easy to stack dependent branches on top of each other.
{% endhint %}

### Creating your first branch

{% hint style="warning" %}
Note that unlike a standard git workflow - where you create a new branch before working on your feature - with `gt` you do the following:

1. Start by building your feature on an existing branch
2. Stage your changes (`gt add -A`)
3. Create a new branch with those changes (`gt branch create`)
{% endhint %}

```bash
gt branch checkout main

# * build feature part 1 *

# create a new branch off of main with your changes and add a commit
gt add -A # add all unstaged change (same syntax as git add)
gt branch create -m "part 1" # -> creates a commit with message "part 1" on a branch named "part_1" (inferred from your branch name) 

# alternatively, you can combine the last 2 commands into a single line:
gt branch create -a -m "part 1" # -> creates a commit with message "part 1" on a branch named "part_1" 
```

{% hint style="info" %}
Because you didn't pass in a branch name in the above example, `gt branch create` auto-generated a branch name from your commit message.  You can configure a prefix for `gt branch create` to add to all of your auto-generated branch names using `gt user branch-prefix` - see the [**CLI command reference**](cli-command-reference.md#user) for more details.
{% endhint %}

### Stack more branches on top

```bash
# * build feature part 2 *

# create a new branch on your stack
gt branch create -a -m "part 2"

# * build feature part 3 *

# create another new branch on your stack
gt branch create -a -m "part 3"
```

Now that you've created a stack, you can use Graphite's CLI to easily visualize it in your terminal.

```
gt log

◉ jg--05-04-part_3 (current)
│ 4 seconds ago
│ * fa0808 - part 3
│
◯ jg--05-04-part_2
│ 27 seconds ago
│ * d4f750 - part 2
│
◯ jg--05-04-part_1
│ 32 seconds ago
│ * 358084 - part 1
│
◯ main
│ 9 days ago
│
```

### Creating a branch without staged changes
Graphite supports creating your branch before starting to code!  In order for Graphite's branch metadata to correctly track dependencies, Graphite will create an empty commit if you create a branch without staged changes, which you are free to either amend or commit on top of with the [**commit-level commands**](updating-a-mid-stack-branch.md).  If you prefer not to amend commits, you can avoid an empty commit in your history with squash-and-merge.


### Branch naming
By default, Graphite will concatenate an optional user prefix, the date, and the commit message to create a branch name that is unlikely to conflict with other branches in your repository.  The prefix can be changed with `gt user branch-prefix`.  For example, in the branch names from the above example, the user's prefix was set to `jg--` with `gt user branch-prefix --set jg--`.  You can also pass a custom name `gt branch create` as a positional argument, e.g.:

```
gt branch create my-branch-for-part-1 -a -m "part 1"
```
