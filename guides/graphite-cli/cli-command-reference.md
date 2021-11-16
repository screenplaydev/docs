# CLI command reference

{% hint style="info" %}
You can always access the full help docs for the Graphite CLI by running `gt --help`
{% endhint %}

```bash
# core commands
gt auth # associates an auth token with your Graphite CLI. This token is used to associate your CLI with your account, allowing us to create and update your PRs on GitHub, for example. To obtain your CLI token, visit https://app.graphite.dev/activate.
gt feedback # post a string directly to the maintainers' Slack, where they can factor in your feedback, laugh at your jokes, cry at your insults, or test the bounds of Slack injection attacks.
gt [log | l] # log all stacks
gt [log short | ls] # log compact view of all stacks
gt [log long | ll] # log extended view of all stacks and commits

# gt branch ...
gt [branch create | bc] <name> # create new stacked branch, commit staged changes
gt [branch next | bn] # traverse upstack by one branch
gt [branch prev | bp] # traverse downstack by one branch
gt branch checkout # interactively check out a branch in your stack, or specify one directly by name, i.e. `gt branch checkout main`
gt branch children # show the child branches of your current branch (i.e. directly above the current branch in the stack) as tracked by Graphite. Branch location metadata is stored under `.git/refs/branch-metadata`.
gt branch parent # show the parent branch of your current branch (i.e. directly below the current branch in the stack) as tracked by Graphite. Branch location metadata is stored under `.git/refs/branch-metadata`.
gt branch land # [COMING SOON] if possible, land branch, clean stack, and fix upstack
gt branch submit # create PR / force push current branch
gt branch top # [COMING SOON] traverse upstack fully
gt branch bottom # [COMING SOON] traverse downstack fully

# gt commit ...
gt [commit create | cc] # create a new commit and fix upstack branches
gt [commit amend | ca] # amend the most recent commit and fix upstack branches

# gt downstack...
gt downstack validate # pull changes to pull request and store in stack metadata, such as titles
gt downstack land # [COMING SOON] attempt to land full stack
gt downstack submit # create pr's / force pushes for full stack

# gt repo...
gt repo init # create or regenerate a `.graphite_repo_config` file.
gt [repo sync | rs] # delete branches in the stack which have been merged into stack trunk
gt repo name # graphite's conception of the current repo's name. e.g. in 'screenplaydev/graphite-cli', this is 'graphite-cli'. Update with "--set <name>"
gt repo owner # graphite's conception of the current repo's owner. e.g. in 'screenplaydev/graphite-cli', this is 'screenplaydev'. Update with "--set <owner>"
gt repo trunk # the trunk branch of the current repo, to use as the base of all stacks. Update with "--set <trunk>"
gt repo max-days-behind-trunk # graphite will track branches that lag up to this many days behind trunk
gt repo max-stacks-behind-trunk # graphite will track up to this many stacks that lag behind trunk

# gt stack ...
gt [stack fix | sf] # choose between --rebase: rebases git branches to match stack, & --regen: create stacks in Graphite based on git branches
gt [stack submit | ss] # create pull requests / force push updates to existing PRs for the current stack
gt stack validate # pull changes to pull request and store in stack metadata, such as titles
gt stack test <command> # [EXPERIMENTAL] Checkout each branch in the stack iteratively, and see if a command succeeds.
gt stack land # [COMING SOON] attempt to land full stack
gt stack fetch # [COMING SOON] pull changes to pull request and store in stack metadata, such as titles

# gt upstack...
gt upstack onto # move upstack inclusive onto some other branch
gt upstack validate # pull changes to pull request and store in stack metadata, such as titles
gt upstack submit # create pr's / force pushes for current branch and children

# gt user...
gt user branch-prefix # view/set a prefix used for prepending new branch names not specified by the user
```
