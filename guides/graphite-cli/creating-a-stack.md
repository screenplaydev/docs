# Creating a stack

{% hint style="info" %}
Graphite's CLI makes it easy to stack dependent branches on top of each other.
{% endhint %}

### Creating your first branch

```bash
gt branch checkout main

# * build feature part 1 *

# create a new branch off of main with your changes and add a commit
gt add -A # add all unstaged change (same syntax as git add)
gt branch create part_1 # -> creates a branch named feat-stories-API
gt commit create -m "part 1" # -> creates a commit with message "part 1"

# alternatively, you can combine the last 3 commands into a single line:
gt branch create -a -m "part 1" # -> Graphite will create a branch name based on your commit message
```

{% hint style="warning" %}
Note that unlike a standard git workflow - where you create a new branch before working on your feature - with `gt` you do the following:

1. Start by building your feature on an existing branch
2. Stage your changes (`gt add -A`)
3. Create a new branch with those changes (`gt branch create`)
{% endhint %}

### Stack more branches on top

```bash
# * build feature part 2 *

# create a new branch on your stack
gt branch create -a -m "part 2"

# * build feature part 2 *

# create another new branch on your stack
gt branch create -a -m "part 3"
```

Now that you've created a stack, you can use Graphite's CLI to easily visualize it in your terminal.
