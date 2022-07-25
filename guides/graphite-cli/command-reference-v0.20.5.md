---
description: >-
  For info about the flags and arguments of any command, just run `gt <command>
  --help`
---

# Command Reference (v0.20.5)

{% hint style="info" %}
The aliases listed in the table are the shortest possible way to invoke each command.  A noun-verb command can be typed all of the following ways:

* `gt branch create`
* `gt b create`
* `gt branch c`
* `gt b c`
* `gt bc`
{% endhint %}

|    auth    |                    |        |                                                         Add your auth token to enable Graphite CLI to create and update your PRs on GitHub.                                                        |
| :--------: | :----------------: | :----: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   branch   |       bottom       |   bb   |                                                                     Switch to the first branch from trunk in the current stack.                                                                    |
|   branch   |      checkout      |   bco  |                                                                                         Switch to a branch.                                                                                        |
|   branch   |       create       |   bc   | Create a new branch stacked on top of the current branch and commit staged changes. If no branch name is specified but a commit message is passed, generate a branch name from the commit message. |
|   branch   |       delete       |   bdl  |                                                                      Delete a branch and its corresponding Graphite metadata.                                                                      |
|   branch   |        down        |   bd   |                                                                             Switch to the parent of the current branch.                                                                            |
|   branch   |        edit        |   be   |                                                       Run an interactive rebase on the current branch's commits and restack upstack branches.                                                      |
|   branch   |        fold        |   bf   |                                        Fold a branch's changes into its parent, update dependencies of descendants of the new combined branch, and restack.                                        |
|   branch   |       rename       |   brn  |                                           Rename a branch and update metadata referencing it. Note that this removes any associated GitHub pull request.                                           |
|   branch   |       restack      |   br   |                                                              Ensure the current branch is based on its parent, rebasing if necessary.                                                              |
|   branch   |        info        |   bi   |                                                                            Display information about the current branch.                                                                           |
|   branch   |        split       |   bsp  |                                                                          Split the current branch into multiple branches.                                                                          |
|   branch   |       squash       |   bsq  |                                                               Squash all commits in the current branch and restack upstack branches.                                                               |
|   branch   |       submit       |   bs   |                                                     Idempotently force push the current branch to GitHub, creating or updating a pull request.                                                     |
|   branch   |         top        |   bt   |                                                                Switch to the tip branch of the current stack. Prompts if ambiguous.                                                                |
|   branch   |        track       |   btr  |                       Start tracking the current branch (by default) with Graphite by selecting its parent. This command can also be used to fix corrupted Graphite metadata.                      |
|   branch   |       untrack      |   but  |                                                   Stop tracking a branch with Graphite. If the branch has children, they will also be untracked.                                                   |
|   branch   |         up         |   bu   |                                                                  Switch to the child of the current branch. Prompts if ambiguous.                                                                  |
|  changelog |                    |        |                                                                                  Show the Graphite CLI changelog.                                                                                  |
|   commit   |        amend       |   ca   |                                                                     Amend the most recent commit and restack upstack branches.                                                                     |
|   commit   |       create       |   cc   |                                                                          Create a new commit and restack upstack branches.                                                                         |
| completion |                    |        |                                                                                 Set up bash or zsh tab completion.                                                                                 |
|  continue  |                    |  cont  |                                                               Continues the most recent Graphite command halted by a merge conflict.                                                               |
|    dash    |                    |    d   |                                                                                       Open the web dashboard.                                                                                      |
|    dash    |         pr         | dp/dpr |                                                                              Opens the PR page for the current branch.                                                                             |
|    docs    |                    |        |                                                                                     Show the Graphite CLI docs.                                                                                    |
|  downstack |        edit        |   dse  |                                              Edit the order of the branches between trunk and the current branch, restacking all of their descendants.                                             |
|  downstack |         get        |   dsg  |                                                Get branches from trunk to the specified branch from remote, prompting the user to resolve conflicts.                                               |
|  downstack |       restack      |   dsr  |                                                    From trunk to the current branch, ensure each is based on its parent, rebasing if necessary.                                                    |
|  downstack |       submit       |   dss  |                               Idempotently force push all branches from trunk to the current branch to GitHub, creating or updating distinct pull requests for each.                               |
|  downstack |        test        |   dst  |                                                From trunk to the current branch, run the provided command on each branch and aggregate the results.                                                |
|  downstack |        track       |  dstr  |                                         Track a series of untracked branches, by specifying each branch's parent, stopping when you reach a tracked branch.                                        |
|  feedback  |                    |        |          Post a string directly to the maintainers' Slack where they can factor in your feedback, laugh at your jokes, cry at your insults, or test the bounds of Slack injection attacks.         |
|  feedback  |    debug-context   |        |                                                             Print a debug summary of your repo. Useful for creating bug report details.                                                            |
|     log    |                    |    l   |                                                            Log all branches tracked by Graphite, showing dependencies and info for each.                                                           |
|     log    |        short       |   ls   |                                                                 Log all stacks tracked by Graphite, arranged to show dependencies.                                                                 |
|     log    |        long        |   ll   |                                                                       Display a graph of the commit ancestry of all branches.                                                                      |
|    repo    |        init        |   ri   |                                                                      Create or regenerate a \`.graphite\_repo\_config\` file.                                                                      |
|    repo    |        name        |        |                                               The current repo's name stored in Graphite. e.g. in withgraphite/graphite-cli', this is 'graphite-cli'.                                              |
|    repo    |        owner       |        |                                           The current repo owner's name stored in Graphite. e.g. in 'withgraphite/graphite-cli', this is 'withgraphite'.                                           |
|    repo    |    pr-templates    |        |                                       A list of your GitHub PR templates. These are used to pre-fill the bodies of your PRs created using the submit command.                                      |
|    repo    |       remote       |        |                                                           Specifies the remote that graphite pushes to/pulls from (defaults to 'origin')                                                           |
|    repo    |        sync        |   rs   |                                                          Pull the trunk branch from remote and delete any branches that have been merged.                                                          |
|    stack   |       restack      |   sr   |                                                       Ensure each branch in the current stack is based on its parent, rebasing if necessary.                                                       |
|    stack   |       submit       |   ss   |                                     Idempotently force push all branches in the current stack to GitHub, creating or updating distinct pull requests for each.                                     |
|    stack   |        test        |   st   |                                                       Run the provided command on each branch in the current stack and aggregate the results.                                                      |
|   upstack  |        onto        |   uso  |                                                Rebase the current branch onto the latest commit of target branch and restack all of its descendants.                                               |
|   upstack  |       restack      |   usr  |                                                Ensure the current branch and each of its descendants is based on its parent, rebasing if necessary.                                                |
|   upstack  |       submit       |   uss  |                                     Idempotently force push the current branch and its descendants to GitHub, creating or updating pull requests as necessary.                                     |
|   upstack  |        test        |   ust  |                                               For each of the current branch and its descendants, run the provided command and aggregate the results.                                              |
|    user    |     branch-date    |        |                                                              Toggle prepending date to auto-generated branch names on branch creation.                                                             |
|    user    |    branch-prefix   |        |                                                                  The prefix which Graphite will prepend to generated branch names.                                                                 |
|    user    | branch-replacement |        |                                                          The character that will replace unsupported characters in generated branch names.                                                         |
|    user    |       editor       |        |                                                                                    The editor opened by Graphite                                                                                   |
|    user    |     submit-body    |        |                                                                                Options for default PR descriptions.                                                                                |
|    user    |        tips        |        |                                                                                   Show tips while using Graphite                                                                                   |
