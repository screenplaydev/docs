# Getting started with Graphite

## Install the CLI

Install the Graphite CLI using npm ([https://www.npmjs.com/](https://www.npmjs.com/)) or Homebrew ([https://brew.sh/](https://brew.sh))

```bash
# Install Graphite from NPM.
npm install -g @withgraphite/graphite-cli

# Or, install Graphite from Homebrew (MacOS)
brew install withgraphite/tap/graphite

# Initialize Graphite.
cd ~/my-project
gt repo init

# Authenticate Graphite CLI via the web dashboard (needed to create PRs).
# Visit https://app.graphite.dev/activate to obtain your auth token and then
# paste it below.
gt auth --token <auth_token>
```

## Sign into the Graphite dashboard

1. Sign in with GitHub at [https://app.graphite.dev/](https://app.graphite.dev)
2. Select one or more of the repos you most frequently work in
3. Graphite will create 6 default sections of pull requests in your repos:
   * **Needs your review** - any PRs where you (or your team) have been tagged as a reviewer
   * **Needs your attention** - your PRs which have been approved or changes have been requested
   * **Waiting for author** - someone else’s PRs which you (or another reviewer) have approved or requested changes on
   * **Waiting for reviewers** - your PRs which are waiting for review
   * **All other pull requests** - all other PRs in the repos you selected

## Join the Graphite Community

By using Graphite, you're joining a community of engineers at top companies around the world who have found stacked changes make them more effective at what they do. Our Graphite Community Slack group is the best place to get support, suggest features, stay up-to-date with our latest releases, and interact with other Graphite beta users and the core team:

{% embed url="https://join.slack.com/t/graphite-community/shared_invite/zt-v828g9dz-TIRvlutxTCqgZmxnsO9Knw" %}

Now that you have Graphite set up, let's walk through an example of how to use the stacked changes workflow.
