# Modifying a stack

With the Graphite CLI, you can easily adjust an existing stack.

### `gt downstack edit`

If you've created a stack of several branches, you can change the order of the stacked branches by using the command `gt downstack edit`.&#x20;

* Checkout the top of the stack you'd like to edit.
* Run `gt downstack edit` to open an interactive editor which shows each branch in the stack as a line.
* Reorder the branches as desired, keeping in mind that you might need to resolve merge conflicts that arise.
* Save and close the file, triggering a series of automated rebases. If conflicts occur: resolve them, stage the resolutions, and run `gt continue` to finish the edit command. This is the same pattern you would use when resolving conflicts in a `gt upstack onto` command.
* After reordering, you can run `gt stack submit` to create PRs or update the merge-bases of existing PRs.

![](../../.gitbook/assets/downstack\_edit\_demo\_large.gif)
