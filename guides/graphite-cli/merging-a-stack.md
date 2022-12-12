# Merging a stack

{% hint style="warning" %}
We find that merging with the Graphite UI saves our engineers - and the engineers that have used it - a substantial amount of time by automating the process of waiting for CI, merging, and rebasing. Anecdotally, we've a number of stories from our users about how they used to block out "half days" just to merge their stacks before using the Graphite UI.

As a result, we strongly recommend merging via the Graphite UI over merging via just the CLI.

If you haven't yet tried it, check out the instructions [here](https://docs.graphite.dev/guides/graphite-dashboard/merging-your-pull-requests#merging-a-stack-of-prs).
{% endhint %}

### Merging a stack via the Graphite dashboard

To merge a stack using the Graphite CLI, we recommend using the "Merge..." button in the [Graphite dashboard](https://app.graphite.dev), which will queue merge jobs for each PR in your stack, automating the process described below.

If you have remaining upstack branches that aren't included in your merge, you'll want to `repo sync --restack` and `submit` after the merge is done.



### Merging a stack via the Graphite CLI

Alternatively, merge the PRs in the stack one at a time:

1. Merge the bottom PR of your stack into your trunk on the [Graphite dashboard](https://app.graphite.dev) (or via GitHub).
2. Run `gt repo sync --restack` from any branch of your stack to pull trunk to local, delete the merged branch, and restack the rest of your stack on trunk.
3. From any branch in your stack, run `gt stack submit` to force push the restacked branches so that the new bottom of your stack can be merged into trunk.
4. Repeat until you've landed all of the branches in your stack.

{% hint style="success" %}
Congratulations - you've landed your stack! Check out the rest of the CLI guide for power user features and to learn about the Graphite dashboard.
{% endhint %}
