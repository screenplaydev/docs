# Installing from source

Some users may want to clone and install the graphite-cli from source.

You'll need git, the latest version of Node.js for your platform and NPM.

Clone & build the Graphite CLI:

```bash
git clone https://github.com/withgraphite/graphite-cli
cd graphite-cli
# git checkout v0.18.0 (we recommend building from the latest version, but this step is optional!)
yarn install
yarn build
```

If you want to install the tool globally:

```bash
sudo npm link
```

Or if you want to install it locally, perhaps just for one user, this can be done by setting a `prefix` before running `npm link`:

```bash
echo "prefix = \"$PWD/.npm-prefix\"" >> .npmrc
npm link

# This has installed `gt` (and its aliases) into `$PWD/.npm-prefix`, which
# you'll now need to add to your `$PATH`. One way to do that is to add it to
# your `.bashrc` (or equivalent for your shell):

echo "" >> $HOME/.bashrc
echo "# Graphite CLI" >> $HOME/.bashrc
echo "export PATH=\$PATH:$PWD/.npm-prefix" >> $HOME/.bashrc
```
