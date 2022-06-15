# Installing the CLI

Install the Graphite CLI using either [npm](https://www.npmjs.com) or [homebrew](https://www.brew.sh):

#### **npm installation**&#x20;

```bash
# Install Graphite from npm.
npm install -g @withgraphite/graphite-cli
gt --version
```

#### **brew installation**

```bash
# Install Graphite from Homebrew.
brew install withgraphite/tap/graphite
gt --version
```

### Node.js versioning

We develop Graphite with and set the Homebrew dependency to Node.js v16 (active LTS version until October 2022), but Graphite should run with no major issues on any current version of Node.  If you run into any issues that seem Node-related, try using v16 if you're able to as a first workaround!

### **Windows**

If you'd like to use Graphite on Windows, we recommend working within Windows Subsystem for Linux.  Follow the [instructions here](https://docs.microsoft.com/en-us/windows/wsl/install) to set it up.  After setting up WSL, you can [set up nvm/node/npm](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl) and then install Graphite as normal!  We are slowly working towards better native Windows support — if you'd like to stay up to date, the discussions are often found in our community Slack.

### **Initialization**

Graphite stores a small JSON configuration file in `.git/.graphite_repo_config` of your repositiory. On first execution (per repository), or by directly running `gt repo init`, the CLI will prompt you to provide a minimal amount of info to populate this config (the trunk branch for your development flow).

```
# Authenticate Graphite CLI via the web dashboard (needed to create PRs).
# Visit https://app.graphite.dev/activate to obtain your auth token and then
# paste it below.
gt auth --token <auth_token>

# Initialize Graphite for your repository
cd ~/my-project
gt repo init
```

After generating the config, the `repo init` offers the option to add existing branches to Graphite by stacking them onto your trunk branch.

Once you've set up the CLI, it's time to authenticate with your GitHub account via the Graphite dashboard.

### Completions

Graphite supports `bash` and `zsh` auto-completion!  After installing Graphite for the first time, you can run (e.g. if using `zsh`, the default on Mac):\
`gt completion >> ~/.zshrc`

For `bash`, you'd replace `.zshrc` with `.bashrc` or `.bash_profile`.\
\
_We don't currently support_ `fish` _completions, but we're looking to — if you're passionate about it, maybe you can help us out with an open source contribution!_
