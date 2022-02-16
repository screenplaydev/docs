# Creating pull requests

{% hint style="info" %}
Once you're finished building, Graphite makes it easy to create pull requests from the branches in your stack.
{% endhint %}

Let's say you're back in our demo repo:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 11.53.30 AM.png>)

Let's check out `review_queue_frontend` and submit the entire stack of 3 branches to GitHub with Graphite:

```bash
# checkout review_queue_frontend
gt bco tr-PK31--review_queue_frontend

# submit the stack to GitHub
gt stack submit
```

`gt stack submit` gives you interactive prompts to help you create pull requests for each branch:

![Edit the PR title](<../../.gitbook/assets/Screen Shot 2021-10-14 at 4.51.22 PM.png>)

![Edit the PR body](<../../.gitbook/assets/Screen Shot 2021-10-14 at 4.51.37 PM.png>)

{% hint style="warning" %}
Graphite selects the text editor for the PR body based on your shell's `$EDITOR` variable.  If you'd like to use a different text editor (i.e. `vim`), make sure to set make sure to set `EDITOR=vim` in your shell before running `gt stack submit`.
{% endhint %}

{% hint style="info" %}
If you have a pull request template saved locally for GitHub, Graphite will automatically detect it and add it to the PR for you to fill out.
{% endhint %}

You can optionally pass `--reviewers` or `-r` to manually specify reviewers for the new pull requests. By default, Graphite will just assign any reviewers specified by [CODEOWNERS files](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) in your repo.

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 4.51.49 PM.png>)

Once you've created pull requests from your stack, Graphite will display the links to view them on the Graphite web dashboard:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 4.52.31 PM.png>)

When running submit for the first time on a stack, or a successive time to push updates, you can use the `--draft/--no-draft` boolean flag to toggle the draft status of PRs in your stack. For example, you might open your PRs initially in draft mode, and then later run `gt stack submit --`no-`draft` to change all PRs in your stack to "ready for review."



Now that you can create pull requests from your stack, you can sync your local repo with remote and keep your stacks up-to-date.
