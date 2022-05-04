# Reviewing pull requests

{% hint style="info" %}
When you click on a PR from a colleague in the review queue, you'll be able to view the proposed changes, add your comments, and submit your review from Graphite.
{% endhint %}

## Timeline, file tree, & Focus Mode

By default, Graphite shows you a timeline of changes, comments, and reviews for a PR in a tray on the right side of the screen:

* Clicking a comment which references a specific line of code will scroll that change into view
* Clicking a commit currently takes you to GitHub, but will soon show the diff for that commit only in Graphite

To show the file tree, click the 🗂 icon in the top right corner of the right-side tray or use the keyboard shortcut `Shift + F`. The file tree shows you the subdirectories of all files changed in a PR:

* Clicking on a changed file will scroll it into view
* New and deleted filenames highlighted green & red respectively

To enter Focus Mode and hide the right side tray altogether, just click the ⏭ icon in the top left of the timeline/file tree tray or use the keyboard shortcut `F`. You can show it again by clicking the "⌄" icon on the PR title bar.

{% hint style="info" %}
You can quickly toggle Focus Mode (show/hide the right-side tray) on the PR page with the keyboard shortcut `F`, show the timeline with `Shift + C`, and show the file tree with `Shift + F`.
{% endhint %}

![Easily show/hide the timeline & file tree as you're reviewing PRs](../../.gitbook/assets/timeline\_and\_file\_tree\_100.gif)

## Adding comments

To add a comment, highlight the lines you want to comment on (you can select one line or multiple lines of code on either side of the diff), enter your comment, and click `Save` (or use `CMD + Enter`). Your comment is now pending - it will show up to you in GitHub as a pending comment, and you can go back and edit it as much as you like before you complete your review (using the review options on the PR title bar).

{% hint style="warning" %}
You need to click one of the review options ("Approve", "Request changes", or "Just add comments") on the PR title bar for pending comments to be shared with the author. This also applies when you're replying to existing comments.
{% endhint %}

Best of all, Graphite enables you to comment anywhere on a PR - not just lines that changed:

!["Out-of-bounds" comments will render perfectly in Graphite, and show a note to the author in GitHub noting the referenced lines](../../.gitbook/assets/comment\_anywhere\_100.gif)

## Adding GIFs & memes to review comments

One of the features we missed the most from Phabricator was the ability to quickly add GIFs & memes to our code reviews to keep them lighthearted and fun. That's why we brought back first-class support for GIFs & memes in Graphite!

![Find the perfect GIF for your review with Giphy, choose one from your team's meme library, or upload a new one](../../.gitbook/assets/gifs\_and\_memes\_100.gif)

Adding a GIF is easy with our Giphy integration:

1. Click the `GIF` icon in the comment box
2. Type in your search text and hit `Enter`
3. Click on the GIF you want to add to your comment, and hit `Save` to see it rendered!

Alternatively, you can select a GIF/meme from your team's meme library:

1. Click the `#` icon in the comment box
2. Click "Browse org macros"
3. Type in your search text, or just click the GIF/meme you want to add to your comment
4. Hit `Save` to see it rendered!

{% hint style="info" %}
Note that every GIF/meme in your team's meme library has a shortcode next to it, which you can use to quickly add it to a review comment with "/". Try typing "/cathack" into a comment to see this in action!
{% endhint %}

Lastly, you can upload your own GIFs & memes to your team's meme library:

* Click the `#` icon in the comment box
* Click "Upload new macro"
* Choose an image/GIF, give it a shortcode, and add it to your comment
* Hit `Save` to see it rendered!

## Reviewing stacked pull requests

Graphite makes it easy to review large stacks of PRs at once. From your PR inbox, just click into a pull request to see the PR details, code changes, and comments. You can always see where the current PR sits and navigate to any of the other PRs in a stack with the "Show stack" button, or by using the keyboard shortcut `S`. Starting from the bottom of the stack, just add your comments, choose your review outcome, and move on to the next PR in the stack!

![Use the stack visualization modal to quickly navigate between PRs in a stack as you review](<../../.gitbook/assets/review\_stacks\_100 (1).gif>)
