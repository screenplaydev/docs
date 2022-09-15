# Squashing, folding, and splitting

### `gt branch squash`

This command squashes multi-commit branches into a single commit branch and restacks upstack branches. Handy if you meant to run `commit create` instead of `commit amend`, or to maintain single-commit branches after folding (see below).

### `gt branch fold`

This command folds (combines) the current branch into its parent, and makes all children of the current branch children of the parent branch instead. It preserves commit history of both branches and their descendants. By default, it will use the name of the parent for the combined branch (the branch being folded into), but you can use the name of the current branch instead with `gt branch fold --keep`

### `gt branch split`

This command splits the current branch into two or more branches. There are two modes of operation: by commit, or by hunk. If there is only one commit on the branch, you will enter `hunk` mode automatically. Otherwise, you can choose a mode by passing in an option. If you do not pass an option, you will be prompted to pick one.

#### `--by-commit`/`--commit`/`-c`

In this mode, you split your branch along already-defined commit boundaries. Eg. if you have a branch with five commits on it, you could put the first three into one branch and the others into another. This preserves commit history of the original branch and its descendants.

[See it in action here.](https://twitter.com/withgraphite/status/1550188212320182273?s=20\&t=vZS81HE4MOOe5FF8SKGuXw)

#### `--by-hunk`/`--hunk`/`-h`

This mode allows you to split your branch by selecting hunks that you'd like to apply to each new branch. The interface is made up of iterative calls to `git add --patch`, which prompts you to stage your changes. You can split your branch by first staging only those you'd like to include in the first branch, then giving it a name, then moving on to the second, giving that one a name, etc.&#x20;

[See it in action here.](https://twitter.com/withgraphite/status/1550188385008029696?s=20\&t=cVtCTfTQH73eyyhsTbG08Q)
