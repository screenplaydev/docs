# Initializing gt in a repo

Graphite stores a small JSON configuration file in `.git/.graphite_repo_config` of your repositiory. On first execution (per repository), or by directly running `gt repo init`, the CLI will prompt you to provide a minimal amount of info to populate this config (the trunk branch for your development flow).

```
# Initialize Graphite for your repository
cd ~/my-project
gt repo init
```

After generating the config, the `repo init` offers the option to add existing branches to Graphite by stacking them onto your trunk branch.  Many users will not need this and just use Graphite for new branches — if that is the case, feel free to skip.

Once you've set up the CLI, it's time to authenticate with your GitHub account via the Graphite dashboard.
