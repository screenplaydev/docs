# Privacy & security

{% hint style="info" %}
Authenticating a new tool with your GitHub account can be scary, so we wanted to be completely transparent about how we integrate with GitHub and make sure your source code is secure.
{% endhint %}

## What data does Graphite store from the GitHub integration?

tl;dr almost nothing.  We've architected our systems to use a minimal amount of data & permissions from our users (within the constraints of GitHub's API), and we'll always be fully transparent about how we use any data and permissions you grant us.

### CLI

Graphite does not store any user source code on its servers from the CLI. When you call `gt stack submit`, the Graphite CLI pushes the branches in your stack to the remote repo in GitHub directly from the client. The only calls from the Graphite server are made to actually open the PRs from the branches which have already been pushed to GitHub. Metadata about which branches were pushed to Github are sent to Graphite servers so we can open those PRs on your behalf.

### Web dashboard

Graphite does not store any source code on its servers from the web dashboard. When you open the dashboard in your browser, it calls GitHub's API directly from the client to retrieve and display pull requests in repos you have access to according to the filter views you've defined. The only data stored on Graphite servers are basic profile metadata (Github ID, username, profile picture) and the auth token generated when you sign in with GitHub, which we use to save your PR filter views and maintain your session.

### Logging

Graphite does not store any user source code on its servers from its logs. During normal usage of the CLI and the website, Graphite will generate and store logs to help us better debug in the event of an error and better understand the profile of our users. Examples of that data include:

* Metadata about your repo: for example, number of branches or counts of Graphite commands being run. We use this to debug failing commands in the CLI (for example, in the past we found a repo with a very high number of branches would cause the CLI to hang.
* Metadata about your usage: for example, commands being run, command runtime, or any CLI errors. We use this to understand where to further our engineering investment and understand how widespread issues are.
* Metadata about your Github account: for example, orgs which you're a member of on Github. We use this to track the usage of our product and understand what types of orgs we work best for.

***

## What permissions does Graphite need from GitHub?

### CLI

You can use the Graphite CLI to manage stacked changes locally without authenticating with your GitHub account - the only command that you need to authenticate to run is `gt stack submit`, which needs to be able to write to the remote repo you're working in to create and/or update pull requests for each branch in your stack.

To authenticate your Graphite CLI:

1. Visit [https://app.graphite.dev/activate](https://app.graphite.dev/activate)
2. Sign in with GitHub to obtain your CLI token
3. Run `gt auth --token <your_token>` in your terminal

### Web dashboard

The [Graphite web dashboard](https://app.graphite.dev) lets you view your queue of pull requests from GitHub. In order to display your PRs, the dashboard needs to be able to read from each repo you want to display PRs for.

When you sign in to the Graphite web dashboard with GitHub for the first time, you can select which organizations and repos to grant access to.

## Using a GitHub Personal Access Token

By default, GitHub prevents third-party applications from automatically creating API tokens for organizations. This can mean that even though you've authenticated Graphite with your GitHub account, we may not be able to generate the token needed to let you create, view, or update your pull requests (if your org has not changed this setting).

For cases such as this one, where you want to give command line tools and APIs limited access to work with your account, GitHub recommends that you create and use [Personal Access Tokens](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) which do have the necessary permissions.

To use a Personal Access Token with Graphite:

1. Generate a new token from your [token settings page on GitHub](https://github.com/settings/tokens) with the following permissions:
   * `repo` (for the repo you want to work in)
   * `read:org`
   * `read:user`
   * `user:email`
2. \[If your org has SSO] Check the [token settings page on GitHub](https://github.com/settings/tokens) and make sure you enable SSO for the Personal Access Token you're using with Graphite.
3. Next, add your new token to Graphite via the [Graphite web dashboard settings page](https://app.graphite.dev/settings).

Once your token is added, you should be able to do the following:

* Select your repo from the dropdowns in each section of the Graphite web dashboard
* Run `gt stack submit` in the Graphite CLI to create pull requests in GitHub for every branch in your stack

If this still doesn't resolve your issue, please ping us on Slack so we can troubleshoot!

***

## What happens if Graphite's GitHub integration changes?

### Process for upcoming changes

We're iterating on Graphite rapidly, but we'll always over-communicate when it comes to how we interact with your source code from GitHub. If we intend to change the architecture or scope of our GitHub integration in the future relating to source code, we'll give you at least 7 days notice prior to making any changes. Furthermore, if we require additional scopes of access from GitHub, you'll be prompted to sign in again with your account and confirm that you want to grant the additional permissions we've requested.

***

### Upcoming changes on our roadmap

In the spirit of transparency, we want to keep you up-to-date on any changes we're currently working on that will change the scope of our integration.

#### Actions from the web dashboard

We soon hope to be able to let developers take actions directly from our dashboard. Two examples of such actions are "land all" (landing multiple dependent PRs) and "revert". In order to enable this functionality, once you press a button to take one of those actions we will spin up an ephemeral container, clone your repo onto it, take the desired action, push the change to Github, and then securely delete the container. Taking this action will clone your source code onto our server, but we will not persist it.

#### Caching

In an effort to reduce our usage of the Github API, we may start caching requests (storing the relevant information on our server). At the moment, we are only intending to cache metadata (e.g. repos which you could access, or information about members of your org to display in hover cards), and we are not intending to cache source code, although we will let you know if this changes.

***

## How does Graphite keep my source code safe?

We understand how important it is to keep your source code safe - that's why we built Graphite with security & privacy best practices from day 1.  We're more than happy to provide you with the following company policies to give you a better sense of how we approach security at Graphite:

* Security Program Overview
* Data Protection Policy
* Security Incident Response Plan
* Encryption Policy
* Vulnerability & Patch Management Policy
* Identity Access Management Policy
* Secure Software Development Policy
* System Audit Policy
* Business Continuity & Disaster Recovery Policy

Please email [**security@graphite.dev**](mailto:security@graphite.dev) to request copies, or feel free to share your team's security questionnaire if you have a standard format.
