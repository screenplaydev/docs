# CLI command reference

{% hint style="info" %}
You can always access the full help docs for the Graphite CLI by running `gt --help`
{% endhint %}

Graphite commands are formatted as noun-verb combinations where the noun is the subject of the command (e.g. `gt branch checkout`).

These nouns include:
* `commit`
* `branch`
* `stack`
* `downstack`
* `upstack`
* `repo`
* `log`
* `user`

## `commit`

{% hint style="info" %}
Where possible, prefer using `commit` commands to using their underlying git equivalents. Graphite's `commit` commands utilize Graphite's understanding of our stack to fix your stack after the commit creation/amend, minimizing merge conflicts.
{% endhint %}

**`gt [commit create | cc]`**
* Create a new commit and fix the upstack branches.
* Options:
  * `-a`<br/>
    `--all`
    * Stage all changes before committing.
  * `-m <message>`<br/>
    `--message <message>`
    * The message for the new commit.

**`gt [commit amend | ca]`**
* Amend the most recent commit and fix the upstack branches.
* Options:
  * `-a`<br/>
    `--all`
    * Stage all changes before committing.
  * `-m <message>`<br/>
    `--message <message>`
    * The updated for the new commit.
  * `--no-edit`
    * Don't modify the existing commit message.

## `branch`

{% hint style="info" %}
All `gt branch` commands can also be accessed by the shortcut `gt b`. 

A select subset of commands also have combined shortcuts, e.g. `gt branch checkout` as `gt bco`, noted below.
{% endhint %}

**`gt [branch create | bc] <name>`**
* Create new stacked branch.
* Options:
  * `-a`<br/>
    `--add-all`
    * Stage all unstaged changes on the new branch.
  * `-m <message>`<br/>
    `--commit-message <message>`
    * Commit staged changes on the new branch with this message.

**`gt [branch checkout | bco]`**
* Interactively check out any branch in the repo.
* Options:
  * `--branch <name>`
    * Check out the specified branch instead, i.e. `gt branch checkout main`.

**`gt [branch next | bn]`**<br/>
**`gt [branch prev | bp]`**
* Traverse upstack/downstack by one branch.
* Options
  * `-n <steps>`<br/>
    `--steps <steps>`
    * Traverse by `n` branches instead.

**`gt branch top`**<br/>
**`gt branch bottom`**
* Traverse to the top/bottom of the stack. If there are multiple paths at any given point in the stack, prompts the user to select which path to take.

**`gt branch children`**<br/>
**`gt branch parent`**
* List the child/parent branches of your current branch as tracked by Graphite.

**`gt branch submit`**
* create PR / force push current branch

## `stack`

{% hint style="info" %}
All `gt branch` commands can also be accessed by the shortcut `gt s`. 

A select subset of commands also have combined shortcuts, e.g. `gt stack submit` as `gt ss`, noted below.
{% endhint %}

**`gt [stack fix | sf]`**
* Fix the stack to match Graphite's knowledge (metadata) of the stack or resets Graphite's stack knowledge to match the current stack DAG.
* Options: 
  * `--rebase`
    * rebase git branches to match Graphite's knowledge of the stack
  * `--regen`
    * reset Graphite's stack knowledge based on current DAG of git branches

**`gt stack validate`**
* Validate that Graphite's stack metadata matches the current DAG of local git branches.

**`gt [stack submit | ss]`**
* Push each branch in the stack to GitHub and open a PR for it into its parent. Prompt the user to input the relevant PR information (e.g. title, body).
* Submit launches an editor to allow you to edit PR info; this editor is controlled by your shell's default `$EDITOR` environment variable.
* Options:
  * `--draft`<br/>
    `--no-draft`
    * Create PRs for the stack in/not in GitHub draft mode.
  * `--no-edit`
    * Skip editing PR info inline; by default, if `--no-edit` is set, the associated PRs will be opened as drafts.
  * `--dry-run`
    * Reports the PRs that would be submitted and terminates. No branches are pushed and no PRs are opened or updated.

**`gt stack test <command>`**
* Checkout each branch in the stack iteratively, and see if a command succeeds.

## `downstack`

Downstack commands operate on the current branch and all of its recursive ancestor branches in the stack (up to trunk).

{% hint style="info" %}
All `gt downstack` commands can also be accessed by the shortcut `gt ds`. 
{% endhint %}

**`gt downstack submit`**<br />
**`gt downstack validate`**
* These commands are equivalent to `gt stack` counterparts (with the same options), but operate only on the downstack (inclusive) branches in the stack.

## `upstack`

Upstack commands operate on the current branch and all of its recursive descendant branches in the stack.

{% hint style="info" %}
All `gt upstack` commands can also be accessed by the shortcut `gt us`. 
{% endhint %}

**`gt upstack submit`**<br />
**`gt upstack validate`**
* These commands are equivalent to `gt stack` counterparts (with the same options), but operate only on the upstack (inclusive) branches in the stack.

**`gt upstack onto <branch>`**
* Rebase all upstack branches onto the latest commit (tip) of the target branch.

## `repo`

## `log`

## `user`