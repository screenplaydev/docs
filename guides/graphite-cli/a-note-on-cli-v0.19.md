# A note on CLI v0.19

If you’re curious to learn more about the changes in this new version of the CLI, read on!

_This page was written to explain the changes to long-standing users of the CLI who are at least a little curious about how Graphite works under the hood — the rest of the documentation has been updated as well._

#### Moving away from the “default-tracked” model

_Historically, the Graphite CLI would by default assume that all branches other than trunk and ignored branches were fair game. This version of the CLI turns this assumption around._

Instead of an ignore list, the new engine requires branches to be explicitly allowlisted with a new command called `gt branch track`. Don’t worry, your current stacks are fine — existing Graphite branches with valid stack metadata will be migrated over cleanly. `gt branch track` is also the command to get a branch back in a valid state if its metadata ever gets corrupted by a Graphite bug or external issue.

The new `repo init` flow walks you through the process of tracking some of your existing local branches when you start using the CLI in a repository.

#### Simplifying restacking

_At their core, most of our local commands perform some operation on your branch or stack, and then automatically rebase each branch in the stack on top of the new version of its parent. We wanted to be clearer about when this is happening and what it actually means._

In this version of the CLI, we have removed the `fix --regen` command and replaced the `fix --rebase` command with a new command called `restack`. The `restack` command can be run on a `branch`, `stack`, `downstack`, or `upstack` (just like `submit`).

The new `restack` operation, for each branch in its scope, ensures that its parent branch is actually in its `git` ancestry, rebasing if necessary. The new engine of the CLI ensures that only commits that are intended to be part of the branch are rebased, as well as reducing the amount of logic that needs to be run in order to check validation state. The end result is the same invariant that prior versions of the CLI enforced — that a PR can only be created/updated when its head branch is correctly situated on its base.

Why remove the `regen` version of `fix`? Quick reminder, `regen` was meant to allow for easily constructing Graphite stacks from “stacks” of git branches that Graphite previously did not know about, or whose Graphite. Now that branches need to be explicitly tracked with `gt branch track`, the new way to do this is to track each branch, specifying its parent as you go!

#### Understanding when it is safe to run `git` commands

_A common ask we get is around interoperability with raw `git` — we hope that the new model of restacking allows us to do this a little better!_

The CLI’s new engine caches all Git and Graphite state in one abstraction with well-enforced invariants. Any time a non-Graphite git command is run between Graphite commands, the cache detects this and invalidates itself.

In addition to this, all restacking that can result in merge conflicts happens at the END of commands. This means that it should generally always be safe to do whatever you want to a branch in between Graphite invocations, as you can always use `restack` to fix your stack before running stack submit.



We hope you enjoy the improvements in both performance and consistency in this new version.  As always, don't hesitate to reach out on our community Slack with any questions!

{% embed url="https://join.slack.com/t/graphite-community/shared_invite/zt-v828g9dz-TIRvlutxTCqgZmxnsO9Knw" %}
