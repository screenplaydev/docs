# Creating pull requests

{% hint style="info" %}
Once you're finished building, Graphite makes it easy to create pull requests from the branches in your stack.
{% endhint %}

Again, let's say we're working with this stack:

![](<../../.gitbook/assets/image (7).png>)

Let's submit the entire stack of 3 branches to GitHub with Graphite:

![](<../../.gitbook/assets/image (13).png>)

`gt stack submit` gives you interactive prompts to help you create pull requests for each branch:

![Edit the PR title](<../../.gitbook/assets/image (8).png>)

![Edit the PR body](<../../.gitbook/assets/image (17).png>)

#### Title Details

For the initial state of the PR title, Graphite will use the title of the first commit on the branch.

#### Body Details

You can configure which text editor to use with Graphite for the PR body by running the command `gt user editor --set` (i.e. `gt user editor --set vim`). By default, Graphite will use your git editor.

For the initial state of the PR body, Graphite will follow the below logic:&#x20;

If you have a pull request template saved locally for GitHub, Graphite will automatically detect it and add it to the PR for you to fill out.

You can also configure Graphite to include your commit message(s) in your PR body with `gt user submit-body --include-commit-messages`.  If you have only one commit in the PR, this will not include the title of the commit (first line of message), as this is already the default title.  If you have multiple commits, all of their messages will be included.

#### Reviewers

You can optionally pass `--reviewers` or `-r` to manually specify reviewers for the new pull requests. By default, Graphite will just assign any reviewers specified by [CODEOWNERS files](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) in your repo.

![Submit with -r specified](<../../.gitbook/assets/image (2).png>)

#### Draft state

Your last option will be whether to submit your PRs as draft or published (ready for review).  You can also pass `--draft` or `--publish` to specify this for all PRs in the submit without having to select each time.  In `--no-interactive` mode,  new PRs will default to draft, and existing PRs will remain in the same state.

{% hint style="info" %}
A common pattern for small changes or to maximize velocity is `gt ss -np` which is the short form of `gt stack submit --no-edit --publish`
{% endhint %}

Once you've created pull requests from your stack, Graphite will display the links to view them on the Graphite web dashboard:

![Final step of submission](<../../.gitbook/assets/image (5).png>)

{% hint style="info" %}
Note that if you need to cancel your submission or it fails for any reason, your PR titles and bodies won't be lost! We cache them locally so they'll be there for when you run `submit` again.
{% endhint %}

`gt stack submit` is also the command for updating your PRs after making changes to your stack!  For example, you might open your PRs initially in draft mode, and then later run `gt stack submit --publish` to change all PRs in your stack to "ready for review."

![Running submit again after making changes](<../../.gitbook/assets/image (9).png>)

Now that you can create pull requests from your stack, you may be wondering how to sync your local repo with remote and keep your stacks up-to-date.

`submit` commands are available in all four scopes: `branch submit`(only submits the current branch), `stack submit`(submits the current branch and all ancestors and descendants), `upstack submit` (submits the current branch and all descendants), and `downstack submit`(submits the current branch and all ancestors).
