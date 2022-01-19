# Using a GitHub Personal Access Token

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

![Here's what your GitHub Personal Access Token settings page should look like when properly set up to use with Graphite](<../../../.gitbook/assets/Screen Shot 2022-01-16 at 6.26.21 PM.png>)

Once your token is added, you should be able to do the following:

* Select your repo from the drop-downs in each section of the Graphite web dashboard
* Run `gt stack submit` in the Graphite CLI to create pull requests in GitHub for every branch in your stack

If this still doesn't resolve your issue, please ping us on Slack so we can troubleshoot!

{% embed url="https://join.slack.com/t/graphite-community/shared_invite/zt-v828g9dz-TIRvlutxTCqgZmxnsO9Knw" %}
