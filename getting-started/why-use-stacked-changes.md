# Why use stacked changes?

{% hint style="warning" %}
Feel free to skip this section if you've worked with stacked changes before!
{% endhint %}

## What is a stack?

A stack is **a sequence of dependent code changes,** each building off of its parent. Stacks enable users to break up a large engineering task into a series of small, incremental code changes, **each of which can be tested, reviewed, and merged independently**.

## Why use stacked changes?

{% hint style="success" %}
**For code authors:**

Stacking changes can help you stay unblocked while you wait for code review, get higher-quality review comments, and land small changes faster.
{% endhint %}

{% hint style="success" %}
**For code reviewers:**

Stacks let you give feedback on small, easy-to-comprehend changes, spend less time re-reviewing, and easily bisect and roll back if something goes wrong.
{% endhint %}

It's no surprise that many of the largest companies have built internal code review platforms which support and encourage engineers to work with stacked changes, such as Critique (Google) & [Phabricator](https://www.phacility.com/phabricator/) (Facebook, Dropbox, Uber, Pinterest, Quora, Twitter). In fact, we missed this workflow so much that we built the first version of Graphite for ourselves as an internal tool to allow us to work with stacked changes on top of GitHub.

## How does Graphite implement stacked changes?

In Graphite, a stack is represented by a directed, acyclic graph (DAG) of dependent git branches. We chose to compose stacks of branches rather than commits because, on GitHub, branches are the smallest discrete unit of CI and code review.

* Graphite extends Git's commits and branches with a third unit - stacks.
* A Graphite stack is a chain (DAG) of dependent branches.
* Graphite tracks stacks by recording parent relationships between branches through git refs.
* Whenever you move a parent branch forward by a commit or rebase it, Graphite uses its persisted metadata to remember the DAG of branches and automatically rebase them to keep your stack up-to-date.

Where is the metadata stored? In your repo in the form of refs, visible at `.git/refs/branch-metadata/`. All information stays within git and can be synced to and from remote repositories.

## References

Plenty of folks smarter than us have written extensively bout the benefits of stacked changes - here are some of our favorite blog posts & papers on the topic:

* [Stacked Diffs Versus Pull Requests](https://jg.gg/2018/09/29/stacked-diffs-versus-pull-requests/)
* [Stacked Diffs: Keeping Phabricator Diffs Small](https://kurtisnusbaum.medium.com/stacked-diffs-keeping-phabricator-diffs-small-d9964f4dcfa6)
* [Problems with Pull Requests and How to Fix Them](https://gregoryszorc.com/blog/2020/01/07/problems-with-pull-requests-and-how-to-fix-them/)
* [Modern Code Review: A Case Study at Google](https://sback.it/publications/icse2018seip.pdf)
* [Real world stack example as a twitter thread](https://twitter.com/benschac/status/1522214962357096448)
