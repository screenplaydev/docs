# Editing the order of branches in a stack

With the Graphite CLI, you can easily modify the dependencies of your branches. After doing so, you'll want to resubmit with `gt stack submit` to push the changes to remote and update the PR dependencies.

### `gt upstack onto`

You can use `gt upstack onto` to rebase a branch and all of its recursive children onto a branch of your choice.

* Checkout the branch that you'd like to rebase.
* Run `gt upstack onto` to open an interactive prompt that allows you to select the new parent of the branch.
* You can also specify the branch yourself with `gt upstack onto new_parent`

### `gt downstack edit`

If you've created a stack of several branches, you can change the order of the stacked branches by using the command `gt downstack edit`.

* Checkout the top of the stack you'd like to edit.
* Run `gt downstack edit` to open an interactive editor which shows each branch in the stack as a line.
* Reorder the branches as desired, keeping in mind that you might need to resolve merge conflicts that arise.
* Save and close the file. This will reorder the branches, first changing the parent pointers, and then performing the necessary restacks. If conflicts occur: resolve them, stage the resolutions, and run `gt continue` to continue restacking. This is the same pattern you would use when resolving conflicts in a `gt upstack onto` command.
* After reordering, you can run `gt stack submit` to create PRs or update the merge-bases of existing PRs.

![](../../.gitbook/assets/downstack\_edit\_demo\_large.gif)

### `gt branch create --insert`

With `--insert`, you can create a new branch based on the current branch and automatically rebase the existing children of the current branch onto the new branch.  You can use `-i` for short:

![](<../../.gitbook/assets/image (10).png>)



