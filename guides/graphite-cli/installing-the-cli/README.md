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

See the following page instructions on setting up shell tab completion after installation.

### Node.js versioning

We develop Graphite with and set the Homebrew dependency to Node.js v16 (active LTS version until October 2022), but Graphite should run with no major issues on any current version of Node.  If you run into any issues that seem Node-related, try using v16 if you're able to as a first workaround!

### **Windows**

If you'd like to use Graphite on Windows, we recommend working within Windows Subsystem for Linux.  Follow the [instructions here](https://docs.microsoft.com/en-us/windows/wsl/install) to set it up.  After setting up WSL, you can [set up nvm/node/npm](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl) and then install Graphite as normal!  We are slowly working towards better native Windows support — if you'd like to stay up to date, the discussions are often found in our community Slack.
