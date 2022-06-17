# Configuration

Graphite offers configuration options both on the global (user) level, and on the repo level.  Note that when run without options, the commands described below display the configured value.

### User-level configuration

Commands found under `gt user`

#### Tips

You can toggle tips with `gt user tips --enable` and `gt user tips --disable`.

#### Editor

By default, Graphite uses the `git` editor for drafting PR descriptions and other flows that require editing text.  You can configure a different editor with `gt user editor --set <editor>`, or revert to using the same editor as `git` with `gt user editor --unset`.

#### Branch naming

If you don't specify a name for your branch (but do specify a commit message) when using `gt branch create`, then Graphite will generate one for based on the commit message.  There are three options to configure here:

1. Whether or not the date is prepended: `gt user branch-date --`\[`enable|disable]`
2. A custom prefix (e.g. initials): `gt user branch-prefix --[set <prefix`>`|reset]`
3. The character with which to replace unsupported symbols (i.e. whitespace and anything other than alphanumeric characters, periods, dashes, underscores, and slashes:
   * `gt user branch-replacement --set-[underscore|dash|empty]`

### Repo-level configuration

Commands found under `gt repo`

#### Git remote name

Graphite defaults to pushing to and pulling from `origin`. if you have configured a different name for your remote, you can set it with:

`gt repo remote --set <value>`

**GitHub repository information**

Graphite infers the GitHub repository name and owner from the remote URL, but in cases where they are not inferred correctly, you can use:

`gt repo [name|owner] --set <value>`

####

####

