# Landing a stack

{% hint style="warning" %}
We're actively working on improving the experience of landing stacks with gt - expect a significantly improved workflow here soon.
{% endhint %}

We are still working on implementing a "land all" operation for merging in stacks and partial stacks. Until then, our recommended workflow for merging in a stack is:

1. Merge the PR at the bottom of the stack into `main` on the [**Graphite dashboard**](https://app.graphite.dev) (or via GitHub).
2. Run `gt repo sync`.
3. Checkout the next PR in your stack (`gt branch next`) and run `gt stack submit` to force push the rebased branch.
4. Repeat until you've landed all of the branches in your stack.

{% hint style="success" %}
Congratulations - you've landed your stack!  Check out the rest of the CLI guide for power user features and to learn about the Graphite dashboard.
{% endhint %}
