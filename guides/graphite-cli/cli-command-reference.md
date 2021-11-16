# CLI command reference

{% hint style="info" %}
You can always access the full help docs for the Graphite CLI by running `gt --help`
{% endhint %}

Graphite commands are formatted as a noun-verb combination where the noun is the subject of the command (e.g. `gt branch checkout`).

These nouns include:
* `commit`
* `branch`
* `stack`
* `downstack`
* `upstack`
* `log`
* `repo`
* `user`

## `commit` Commands

{% hint style="info" %}
Where possible, prefer using `commit` commands to using their underlying git equivalents. Graphite's `commit` commands utilize Graphite's understanding of our stack to fix your stack after the commit creation/amend, minimizing merge conflicts.
{% endhint %}

`gt [commit create | cc]` 

* Create a new commit and fix the upstack branches.
* Options:
  * `-a`<br/>
    `--all`<br/>
    Stage all changes before committing.
  * `-m <message>`<br/>
    `--message <message>`<br/>
    The message for the new commit.

`gt [commit amend | ca]`
* Amend the most recent commit and fix the upstack branches.
* Options:
  * `-a`<br/>
    `--all`<br/>
    Stage all changes before committing.
  * `-m <message>`<br/>
    `--message <message>`<br/>
    The updated for the new commit.
  * `--no-edit`<br/>
    Don't modify the existing commit message.

## `branch` Commands

All `gt branch` commands can be accessed by the shortcut `gt b` instead. 

A select subset of commands also have combined shortcuts, e.g. `gt branch checkout` as `gt bco`, noted below.

`gt [branch create | bc] <name>` 
* Create new stacked branch.
* Options:
  * `-a`<br/>
    `--add-all`<br/>
    Stage all unstaged changes on the new branch.
  * `-m <message>`<br/>
    `--commit-message <message>`<br/>
    Commit staged changes on the new branch with this message.

`gt [branch checkout | bco]` 
* Interactively check out any branch in the repo.
* Options:
  * `--branch <name>`<br/>
    Check out the specified branch instead, i.e. `gt branch checkout main`.

`gt [branch next | bn]`<br/>
`gt [branch prev | bp]` 
* Traverse upstack/downstack by one branch.
* Options
  * `-n <steps>`<br/>
    `--steps <steps>`<br/>
    Traverse by `n` branches instead.

`gt branch top`<br/>
`gt branch bottom`
* Traverse to the top/bottom of the stack. If there are multiple paths at any given point in the stack, prompts the user to select which path to take.

`gt branch children`<br/>
`gt branch parent`
* List the child/parent branches of your current branch as tracked by Graphite.

`gt branch submit` 
* create PR / force push current branch