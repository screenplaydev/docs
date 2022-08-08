# Configuration

Graphite offers configuration options both on the global (user) level, and on the repo level.  Note that when run without options, the commands described below display the configured value.

### User-level configuration

Commands found under `gt user`. Use `gt user --help` to see all options from the CLI.

#### Tips

You can toggle tips with `gt user tips --enable` and `gt user tips --disable`.

#### Editor

By default, Graphite uses the `git` editor for drafting PR descriptions and other flows that require editing text.

You can configure a different editor with `gt user editor --set <editor>`, or revert to using the same editor as `git` with `gt user editor --unset`.

#### Pager

By default, Graphite uses the `git` pager for drafting PR descriptions and other flows that require editing text.

You can configure a different pager with `gt user pager --set <pager>`, or revert to using the same pager as `git` with `gt user editor --unset`.

You can disable paging entirely with `gt user pager --disable`.

Note that just like `git`, Graphite sets the environment variables `LESS=FRX` and `LV=-c` if they are not already set.  If something else is setting your `LESS` env var, you can use `gt user pager --set "less -FRX"` to get the recommended pager settings.&#x20;

#### Branch naming

If you don't specify a name for your branch (but do specify a commit message) when using `gt branch create`, then Graphite will generate one for based on the commit message.  There are three options to configure here:

1. Whether or not the date is prepended: `gt user branch-date --`\[`enable|disable]`
2. A custom prefix (e.g. initials): `gt user branch-prefix --[set <prefix`>`|reset]`
3. The character with which to replace unsupported symbols (i.e. whitespace and anything other than alphanumeric characters, periods, dashes, underscores, and slashes:
   * `gt user branch-replacement --set-[underscore|dash|empty]`

#### Submit PR body

Graphite can include the commit messages of your branch in the body of your PR automatically on submit.  Enable this with `gt user submit-body --include-commit-messages` and disable with `gt user submit-body --no-include-commit-messages`.  Note that if you only have a single commit on your branch, the first line of the message (i.e. its title) will not be included as this is already the default for the name of the PR.

#### Committer date on rebase

The `git rebase` flag `--committer-date-is-author-date` is useful if you don't want your Graphite restack operations to update the committer date of the commits in your branches.  In order to have Graphite's internal rebases use this flag, you can enable the configuration `gt user restack-date --use-author-date`.  To turn this back off, use `gt user restack-date --no-use-author-date`





### Repo-level configuration

Commands found under `gt repo`. Use `gt repo --help` to see all options from the CLI.

#### Git remote name

Graphite defaults to pushing to and pulling from `origin`. if you have configured a different name for your remote, you can set it with:

`gt repo remote --set <value>`

**GitHub repository information**

Graphite infers the GitHub repository name and owner from the remote URL, but in cases where they are not inferred correctly, you can use:

`gt repo [name|owner] --set <value>`

####

####

