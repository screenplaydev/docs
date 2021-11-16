# Authenticating the CLI

{% hint style="info" %}
If you want to use Graphite to create or update pull requests in GitHub for the branches in your stack using `gt stack submit`, you'll need to authenticate the CLI with your GitHub account.
{% endhint %}

Authenticating the Graphite CLI is easy:

1. Sign into [https://app.graphite.dev/activate](https://app.graphite.dev/activate) with your GitHub account
2. Copy the `gt auth --token <your_cli_auth_token>` command shown (your CLI auth token will be pre-filled)
3. Paste & run it in your terminal

Once you've authenticated the CLI, you should be able to run `gt stack submit` to create or update pull requests in GitHub for every branch in your stack.

Your privacy & security are top priorities - Graphite is architected to ask for the minimum set of permissions necessary within the constraints of GitHub's API.  Learn more our GitHub integration here:

{% content-ref url="../../../getting-started/privacy-and-security.md" %}
[privacy-and-security.md](../../../getting-started/privacy-and-security.md)
{% endcontent-ref %}

## Troubleshooting

Depending on your organization's settings, you may see the following error when you run `gt stack submit`:

```
"Third-party access" > "Third-party application access policy" is set to 
"Access restricted" (GitHub default) in your organization's settings,
meaning that Graphite cannot submit PRs on your behalf using your standard 
OAuth token.
```

If you still want to use `gt stack submit`, you can add a [GitHub Personal Access Token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) (these are intended to give command line tools limited access to work with your account) - just follow these instructions to enable access:

{% content-ref url="using-a-github-personal-access-token.md" %}
[using-a-github-personal-access-token.md](using-a-github-personal-access-token.md)
{% endcontent-ref %}

Once you've added your Personal Access Token to the web dashboard, the Graphite CLI will automatically pick it up (you don't need to run `gt auth` again), and `gt stack submit` should work correctly.

