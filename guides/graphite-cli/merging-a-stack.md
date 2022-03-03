# Merging a Stack

{% hint style="warning" %}
We find that merging with the Graphite UI saves our engineers - and the engineers that have used it - a substantial amount of time by automating the process of waiting for CI, merging, and rebasing. Anecdotally, we've a number of stories from our users about how they used to block out "half days" just to merge their stacks before using the Graphite UI.

As a result, we strongly recommend merging via the Graphite UI over merging via just the CLI.

If you haven't yet tried it, check out the instructions [here](https://docs.graphite.dev/guides/graphite-dashboard/merging-your-pull-requests#merging-a-stack-of-prs).
{% endhint %}

To merge a stack using the Graphite CLI:

1. Merge the PR at the bottom of the stack into `main` on the [Graphite dashboard](https://app.graphite.dev) (or via GitHub).
2. Run `gt repo sync`.
3. Checkout the next PR in your stack (`gt branch next`) and run `gt stack submit` to force push the rebased branch.
4. Repeat until you've landed all of the branches in your stack.

{% hint style="success" %}
Congratulations - you've landed your stack! Check out the rest of the CLI guide for power user features and to learn about the Graphite dashboard.
{% endhint %}
