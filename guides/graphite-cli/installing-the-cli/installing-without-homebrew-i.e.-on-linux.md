# Installing without Homebrew (i.e. on Linux)

To install the Graphite CLI without Homebrew (on Linux for example):

```bash
# first, install the latest version of node

# install the Graphite CLI
git clone https://github.com/screenplaydev/graphite-cli
cd graphite-cli
npm install
npm run build
npm link

# you should now have the gt command line tool installed!
```

Thanks to Sean Behan for writing up these instructions!
