# Installing the CLI

Install the Graphite CLI using either [npm](https://www.npmjs.com) or [homebrew](https://www.brew.sh):

#### **npm installation**&#x20;

```bash
# Install Graphite from npm.
npm install -g @withgraphite/graphite-cli
gt --version
```

#### **brew installation (on MacOS)**

```bash
# Install Graphite from Homebrew.
brew install withgraphite/tap/graphite
gt --version
```

### **Initialization**

Graphite stores a small JSON configuration file in `.git/.graphite_repo_config` of your repository. On first execution, the CLI will prompt you to provide a minimal amount of info to populate this config.

```
# Initialize Graphite.
cd ~/my-project
gt repo init

# Authenticate Graphite CLI via the web dashboard (needed to create PRs).
# Visit https://app.graphite.dev/activate to obtain your auth token and then
# paste it below.
gt auth --token <auth_token>
```

Once you've set up the CLI, it's time to authenticate with your GitHub account via the Graphite dashboard.
