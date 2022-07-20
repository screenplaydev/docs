# Troubleshooting

If you find yourself in a seemingly bad state, please submit a bug report with metadata by running:\
`gt feedback --with-debug-context <`your-`message-here>` so that we can reproduce and fix your issue in the general case!\
\
To unblock yourself locally you have a few options:

\
`gt dev cache --clear` is a command that shouldn't ever need to be run, but is totally safe, doesn't change any git or graphite state and sometimes fixes inadvertent issues that we haven't caught before release.

If that doesn't work, and you would like specific help for your issue, give us a shout on our [Community slack channel](https://join.slack.com/t/graphite-community/shared\_invite/zt-1as9rdo7r-pYmEZzt6M1EhTkvJFNhsnQ).

You can also try to fix your state manually if you're brave and can't wait:

Use `gt branch untrack` to stop tracking any affected branches with Graphite, then use a combination of `git rebase`, `gt downstack track` and `gt branch track` to get your repo back in working order.  The extreme of this is `gt repo init --reset` which will reset all Graphite metadata such that all branches will need to be re-tracked.
