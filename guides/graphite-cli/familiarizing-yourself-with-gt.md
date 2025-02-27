# Familiarizing yourself with gt

Welcome to Graphite! Once you've installed the CLI, it's time to start learning the core commands and workflow.\
\
We'll start with the basics of creating a stack of changes, submitting the changes for review, addressing comments, and merging them.  Later on in the guide, we'll get into other topics including reordering stacked branches and collaborating on stacks with your teammates.

### Commands

Graphite's commands (for the most part) follow a noun-verb model, i.e. `gt branch create` creates a branch.  We'll go over most commands in the following pages. If you at any time need help remembering a command, how it works, or what the shortcuts are, we do our best to provide a multitude of ways to unblock yourself:

* `--help` options for every command
  * Run `gt --help` to see the list of top-level commands (mostly nouns)
  * Run `gt <noun> --help` to see the list of commands (verbs) for a given noun
  * Run `gt <command> --help` to see all options that can be passed to the command
* Tab completion (see the "Shell completion setup" page under "Installing the CLI")
* The "Command reference" page found at the end of this guide.

{% hint style="info" %}
Graphite's CLI features a **git passthrough** - `gt` will pass any unrecognized commands thru to `git`, so you can run commands like `gt add`or `gt status`, even though they aren't native commands in `gt`.\
\
Git passthrough helps to avoid confusion about when to use `gt` vs. `git` - you should be able to use `gt` for everything in your git workflow. [Learn more here](https://docs.graphite.dev/guides/graphite-cli/mixing-gt-and-git).
{% endhint %}

### Definitions

**Stack**: A series of `git` branches that depend on each other.  Starts at `main` (or whatever your trunk branch may be called), and proceeds "upward" as dependent branches are stacked on. Commands within the "stack" noun operate on all ancestors and descendants of a branch.

**Upstack**: branches further away from `main` in a stack (more recent; descendants; recursive children).  Commands within the "upstack" noun operate on a branch and descendants.

**Downstack**: branches closer to `main` in a stack (less recent; ancestors; recursive parents). Commands within the "downstack" noun operate on a branch and its ancestors.

If you're still a little confused about what these actually mean in practice, don't worry! Just keep reading and it'll all make sense soon enough.

### More help

If you ever run into trouble figuring something out, or have a suggestion on how this documentation might be improved, please reach out in our community Slack channel.

{% embed url="https://join.slack.com/t/graphite-community/shared_invite/zt-1as9rdo7r-pYmEZzt6M1EhTkvJFNhsnQ" %}
