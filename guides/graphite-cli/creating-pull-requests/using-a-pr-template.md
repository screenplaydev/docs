# Using a PR template

As mentioned on the previous page, the Graphite CLI tries to include any PR template that might be present in the repository in the default body. The logic mimics GitHub's:

All PR templates must be located in

1. The top-level of the repository.
2. A `.github/` directory.
3. A `.docs/` directory.

GitHub allows you to define a single default PR template by naming it `pull_request_template` (case-insensitive) with either a `.md` or `.txt` file extension. If one of these is provided, GitHub autofills the body field on the PR creation page — unless it is overridden with a template query param. If you have multiple PR templates, you can put them in a `PULL_REQUEST_TEMPLATE` directory in one of the PR locations above. However, at PR creation time, GitHub doesn't autofill the body field on the PR creation page unless you tell it which template to use via a URL query param.

**Sources:**

****[https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)

[https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)

{% hint style="info" %}
If `submit` finds only one template, it will use that one.  If it finds multiple, it will prompt for selection.
{% endhint %}

