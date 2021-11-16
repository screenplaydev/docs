# Installing the CLI

Install the Graphite CLI using Homebrew ([https://brew.sh/](https://brew.sh))

```bash
# install Graphite from Homebrew
brew install screenplaydev/tap/graphite

# initialize Graphite
cd ~/my-project
gt repo init

# authenticate Graphite CLI via the web dashboard (needed to create PRs)
gt auth
```

If you can't install Graphite via Homebrew (i.e. you develop on Linux), you can still use Graphite by following these steps:

{% content-ref url="installing-without-homebrew-i.e.-on-linux.md" %}
[installing-without-homebrew-i.e.-on-linux.md](installing-without-homebrew-i.e.-on-linux.md)
{% endcontent-ref %}



Once you've set up the CLI, it's time to authenticate with your GitHub account via the Graphite dashboard.
