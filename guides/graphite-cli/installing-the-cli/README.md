# Installing the CLI

Install the Graphite CLI using either Homebrew ([https://brew.sh/](https://brew.sh)) or npm:



#### **Homebrew installation**

```bash
# Install Graphite from Homebrew.
brew install withgraphite/tap/graphite
gt --version
```

#### **npm installation**

```bash
# Install Graphite from npm.
npm install -g @withgraphite/graphite-cli
gt --version
```

#### ****

#### **Initialization**

Graphite stores a small JSON configuration file in `.git/.graphite_repo_config` of your repositiory. On first execution, the CLI will prompt you to provide a minimal amount of info to populate this config.

```
# Initialize Graphite.
cd ~/my-project
gt repo init

# Authenticate Graphite CLI via the web dashboard (needed to create PRs).
# Visit https://app.graphite.dev/activate to obtain your auth token and then
# paste it below.
gt auth --token <auth_token>
```



You can install Graphite from source by following the below instructions.  Note that there may be occasional bugs on trunk — please check out a release branch!

{% content-ref url="installing-from-source.md" %}
[installing-from-source.md](installing-from-source.md)
{% endcontent-ref %}

Once you've set up the CLI, it's time to authenticate with your GitHub account via the Graphite dashboard.
