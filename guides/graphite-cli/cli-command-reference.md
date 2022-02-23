# CLI command reference

{% hint style="info" %}
You can always access the full help docs for the Graphite CLI by running `gt --help`
{% endhint %}

Graphite commands are formatted as noun-verb combinations where the noun is the subject of the command (e.g. `gt branch checkout`).

These nouns include:

* [`commit`](cli-command-reference.md#commit)
* [`branch`](cli-command-reference.md#branch)
* [`stack`](cli-command-reference.md#stack)
* [`downstack`](cli-command-reference.md#downstack)
* [`upstack`](cli-command-reference.md#upstack)
* [`repo`](cli-command-reference.md#repo)
* [`log`](cli-command-reference.md#log)
* [`user`](cli-command-reference.md#user)
* [`feedback`](cli-command-reference.md#feedback)
* [`auth`](cli-command-reference.md#auth)

At a glance, we find that the most commonly useful commands for users to know are:

* Fetching Changes (e.g. `git pull`)
  * `gt repo sync`
* Creating Changes
  * `gt branch create`
  * `gt commit create`
  * `gt commit amend`
* Rebasing
  * `gt stack fix`
  * `gt upstack onto`
* Submitting Changes
  * `gt stack submit`
  * `gt downstack submit`
  * `gt upstack submit`
* Misc
  * `gt log`
  * `gt feedback`

## `commit`

{% hint style="info" %}
Where possible, prefer using `commit` commands to using their underlying git equivalents. Graphite's `commit` commands utilize Graphite's understanding of our stack to fix your stack after the commit creation/amend, minimizing merge conflicts.
{% endhint %}

**`gt commit create` \*\* or \*\* `gt cc`**

Create a new commit and fix the upstack branches.

* Options:
  * `-a`\
    `--all`
    * Stage all changes before committing.
  * `-m <message>`\
    `--message <message>`
    * The message for the new commit.

**`gt commit amend` \*\* or \*\* `gt ca`**

* Amend the most recent commit and fix the upstack branches.
* Options:
  * `-a`\
    `--all`
    * Stage all changes before committing.
  * `-m <message>`\
    `--message <message>`
    * The updated for the new commit.
  * `--no-edit`
    * Don't modify the existing commit message.

## `branch`

{% hint style="info" %}
All `gt branch` commands can also be accessed by the shortcut `gt b`.

A select subset of commands also have combined shortcuts, e.g. `gt branch checkout` as `gt bco`, noted below.
{% endhint %}

**`gt branch create <name>` \*\* or \*\* `gt bc <name>`**

* Create new stacked branch.
* Options:
  * `-a`\
    `--add-all`
    * Stage all unstaged changes on the new branch.
  * `-m <message>`\
    `--commit-message <message>`
    * Commit staged changes on the new branch with this message.

**`gt branch checkout` \*\* or \*\* `gt bco`**

* Interactively check out any branch in the repo.
* Options:
  * `--branch <name>`
    * Check out the specified branch instead, i.e. `gt branch checkout main`.

**`gt branch next` \*\* or \*\* `gt bn`**\
**`gt branch prev` \*\* or \*\* `gt bp`**

* Traverse upstack/downstack by one branch.
* Options
  * `-n <steps>`\
    `--steps <steps>`
    * Traverse by `n` branches instead.

**`gt branch top`**\
**`gt branch bottom`**

* Traverse to the top/bottom of the stack. If there are multiple paths at any given point in the stack, prompts the user to select which path to take.

**`gt branch children`**\
**`gt branch parent`**

* List the child/parent branches of your current branch as tracked by Graphite.

**`gt branch submit`**

* create PR / force push current branch

## `stack`

{% hint style="info" %}
All `gt stack` commands can also be accessed by the shortcut `gt s`.

A select subset of commands also have combined shortcuts, e.g. `gt stack submit` as `gt ss`, noted below.
{% endhint %}

**`gt stack fix` \*\* or \*\* `gt sf`**

* Fix the stack to match Graphite's knowledge (metadata) of the stack or resets Graphite's stack knowledge to match the current stack DAG.
* Options:
  * `--rebase`
    * rebase git branches to match Graphite's knowledge of the stack
  * `--regen`
    * reset Graphite's stack knowledge based on current DAG of git branches

**`gt stack validate`**

* Validate that Graphite's stack metadata matches the current DAG of local git branches.

**`gt stack submit` \*\* or \*\* `gt ss`**

* Push each branch in the stack to GitHub and open a PR for it into its parent. Prompt the user to input the relevant PR information (e.g. title, body).
* Submit launches an editor to allow you to edit PR info; this editor is controlled by your shell's default `$EDITOR` environment variable.
* Options:
  * `--draft`\
    `--no-draft`
    * Create or update PRs for the stack in/not in GitHub draft mode.
  * `--no-edit`
    * Skip editing PR info inline; by default, if `--no-edit` is set, the associated PRs will be opened as drafts.
  * `--dry-run`
    * Reports the PRs that would be submitted and terminates. No branches are pushed and no PRs are opened or updated.
  * `--reviewers`
    * Manually specifiy the reviewers for new PRs

**`gt stack test <command>`**

* Checkout each branch in the stack iteratively, and see if a command succeeds.

## `downstack`

Downstack commands operate on the current branch and all of its recursive ancestor branches in the stack (up to trunk).

{% hint style="info" %}
All `gt downstack` commands can also be accessed by the shortcut `gt ds`.
{% endhint %}

**`gt downstack submit`**\
**`gt downstack validate`**

* These commands are equivalent to `gt stack` counterparts (with the same options), but operate only on the downstack (inclusive) branches in the stack.

## `upstack`

Upstack commands operate on the current branch and all of its recursive descendant branches in the stack.

{% hint style="info" %}
All `gt upstack` commands can also be accessed by the shortcut `gt us`.
{% endhint %}

**`gt upstack submit`**\
**`gt upstack validate`**

* These commands are equivalent to `gt stack` counterparts (with the same options), but operate only on the upstack (inclusive) branches in the stack.

**`gt upstack onto <branch>`**

* Rebase all upstack branches onto the latest commit (tip) of the target branch.

## `repo`

{% hint style="info" %}
All `gt repo` commands can also be accessed by the shortcut `gt r`.
{% endhint %}

**`gt repo init`**

* Initialize/re-initialize Graphite in the current git repository. Default mode for this command is interactive and you will be prompted for specifying your trunk branch and branches to ignore.
* Init configurations are stored in the `.git/.graphite_repo_config` file.
* Options
  * `--trunk`
    * The name of your trunk branch.
  * `--ignore-branches`
    * A list of branches (or glob patterns) that Graphite should ignore when tracking your stacks (i.e. branches you never intend to merge into trunk).

**`gt repo ignored-branches`**

* Specify glob patterns matching branch names for Graphite to ignore. Often branches that you never plan to create PRs and merge into trunk.
* This configuration is stored in the `.git/.graphite_repo_config` file inside your repo directory.
* Options
  * `--add`
    * Add a branch or glob pattern to be ignored by Graphite.
  * `--remove`
    * Remove a branch or glob pattern from being ignored by Graphite.

**`gt repo sync` \*\* or \*\* `gt rs`**

* Sync with remote and delete branches in the stack which have been merged into stack trunk, rebasing any unmerged upstack changes, also offering to resubmit PRs with changed bases and repair dangling Graphite branches.
* Options
  * `--show-delete-progress`
    * Show a rough estimate of progress through deleting branches. (This is commonly used by users running `gt repo sync` in a long-standing git repo with tens/hundreds of dead branches where Graphite has just been initialized.)
  * `-f`\
    `--force`
    * Skip prompting to delete feature branches that have been merged into trunk, and suggesting resubmission of branches whose PR bases differ locally from remote. Instead, Graphite will take the default actions. To override default options, use one of the additional flags like `--no-delete` or `--no-resubmit`
  * `--no-pull`
    * Skip the step where Graphite pulls from remote.
  * `--no-delete`
    * Skip the step where Graphite checks whether feature branches have been merged into trunk and suggests deleting them.
  * `--no-resubmit`
    * Skip the step where Graphite suggests resubmitting branches whose PR bases differ locally from remote (often because they've been since rebased locally).
  * `--no-show-dangling`
    * Skip the step where Graphite checks for dangling branches (i.e. without a tracked parent in Graphite). Dangling branches are often the cause of mysterious bugs in Graphite behavior.

**`gt repo fix`**

* Search for and remediate common problems in your repo that slow Graphite down and/or cause bugs.
* Commonly remediated problems include: stale branches, branches with unknown parents.
* Options
  * `--show-delete-progress`
    * Show a rough estimate of progress through deleting branches. (This is commonly used by users running `gt repo sync` in a long-standing git repo with tens/hundreds of dead branches where Graphite has just been initialized.)
  * `-f`\
    `--force`
    * Skip prompting to delete feature branches that have been merged into trunk. Instead, Graphite will take the default actions (may include deleting already merged branches and setting branch parents).

**`gt repo max-branch-length`**

* Print the setting value of `gt repo max-branch-length`. Graphite will track up to this many commits on a branch. e.g. If this is set to 50, Graphite can track branches up to 50 commits long.
* Increasing this setting will increase the accuracy of Graphite in repos with branches with many commits, but may result in slower Graphite performance.
* Options:
  * `--set <max-branch-length>`
    * Set the value of `max-branch-length`.

**`gt repo max-days-behind-trunk`**

* Print the setting value of `max-days-behind-trunk`. Graphite will track branches up to `max-days-behind-trunk` days behind trunk.
* This is often used in repos where users have a plethora of local branches behind trunk causing slow Graphite performance.
* Options:
  * `--set <max-days-behind-trunk>`
    * Set the value of `max-days-behind-trunk`.

**`gt repo max-stacks-behind-trunk`**

* Print the setting value of `max-stacks-behind-trunk`. Graphite will track the most recent `max-stacks-behind-trunk` number of stacks behind trunk.
* Options:
  * `--set <max-stacks-behind-trunk>`
    * Set the value of `max-stacks-behind-trunk`.

**`gt repo name`**

* Print Graphite's understanding of the current repo name. e.g. in 'screenplaydev/graphite-cli', this is 'graphite-cli'.
* Options:
  * `--set <name>`
    * Add a manual override to Graphite's inferred repo name.

**`gt repo owner`**

* Print Graphite's understanding of the current repo owner. e.g. in 'screenplaydev/graphite-cli', this is 'screenplaydev'.
* Options:
  * `--set <owner>`
    * Add a manual override to Graphite's inferred repo owner.

**`gt repo trunk`**

* Print Graphite's understanding of the trunk branch of the current repo. This trunk branch is used interally in Graphite as the base of all stacks.
* Options:
  * `--set <trunk>`
    * Add a manual override to Graphite's inferred repo trunk.

**`gt repo pr-templates`**

* Lists Graphite's view of the repo's GitHub PR templates. These PR templates are in turn used to pre-populate the body content of a PR when a user runs a gt submit command.

## `log`

{% hint style="info" %}
All `gt log` commands can also be accessed by the shortcut `gt l`.
{% endhint %}

**`gt log`**\
**`gt log short`**\
**`gt log long`**

* Print a visualization of the current repo's stacks in the command line.
* Options:
  * `-t`\
    `--on-trunk`
    * Only print commits and branches on trunk.
  * `-b`\
    `--behind-trunk`
    * Only print commits and branches behind trunk.

## `user`

**`gt user branch-prefix`**

* Print the setting value of `branch-prefix`. Graphite will prepend this prefix to all auto-generated branch names (i.e. when you don't specify a branch name when calling `gt branch create`).
* Options:
  * `--set <branch-prefix>`
    * Set the value of `branch-prefix` (string).

**`gt user tips`**

* Print whether Graphite tips are enabled.
* Options:
  * `--enable`
    * Enable tips.
  * `--disable`
    * Disable tips.

## `feedback`

**`gt feedback`**

* Post a string directly to the maintainers' Slack, where they can factor in your feedback, laugh at your jokes, cry at your insults, or test the bounds of Slack injection attacks.
* Options:
  * `--with-debug-context`
    * Include a blob of JSON describing your repo's state to help with debugging. Run `gt feedback state` to see what's included.

## `auth`

**`gt auth`**

* Associate an auth token with your Graphite CLI. This token is used to associate your local CLI instance with your Graphite account, allowing us to create and update PRs on GitHub on your behalf. To obtain your CLI token, visit https://app.graphite.dev/activate.
* Options:
  * `--token`
    * Auth token value to save.
