# Using Graphite on Windows (via WSL)

While we don't yet fully support the Graphite CLI on Windows, many users have started working with Graphite on Windows via WSL with the following steps:

1. Install WSL ([https://docs.microsoft.com/en-us/windows/wsl/install](https://docs.microsoft.com/en-us/windows/wsl/install))
2. Install brew ([https://docs.brew.sh/Homebrew-on-Linux](https://docs.brew.sh/Homebrew-on-Linux))
3. Install graphite-cli (`brew install screenplaydev/tap/graphite`)
4. From a WSL terminal navigate to your project on windows filesystem (`cd /mnt/c/<path to project`)
5. Initialize Graphite (`gt repo init`)
6. Authenticate the Graphite CLI (get your token from [https://app.graphite.dev/activate](https://app.graphite.dev/activate), then run `gt auth --token <auth_token>`)

Thanks to Ludovic Fardel for figuring out & writing up these instructions!
