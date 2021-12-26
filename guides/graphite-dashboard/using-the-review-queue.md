# Using the review queue

## Sorting pull requests

Each pull request that matches the filters for each section will show up in the table:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 7.44.12 PM.png>)

You can sort by title, change size, and last updated time.

## Searching pull requests

You can also search for pull requests (by title, author etc) using the search icon in the upper right corner of each section:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 8.00.19 PM.png>)

## Pull request info

Each PR in the table has (from left to right):

* Approval status (has the PR been approved?)
* Title & author
* Position in stack
* CI status (is CI passing/failing/in progress?)
* Mergable status (are there conflicts with `main`?)
* Lines added/deleted
* Last updated time (by default, the table is sorted by most recently updated)

Clicking each row will take you to the Graphite code review interface for the pull request - more info here:

{% content-ref url="reviewing-code-with-graphite-alpha.md" %}
[reviewing-code-with-graphite-alpha.md](reviewing-code-with-graphite-alpha.md)
{% endcontent-ref %}

## Understanding stacks

Clicking on the `4/5` in the above example PR opens a modal where you can see where the PR is in a stack:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 7.47.03 PM.png>)

Note that you can see the status of each PR (in this case all are drafts) - here's another example with an approved PR at the top of the stack, but changes requested on the bottom PR:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 7.47.09 PM.png>)

##
