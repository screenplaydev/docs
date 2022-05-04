# Navigating a stack

{% hint style="info" %}
Let's say this is the state of your repo - Graphite makes it easy to navigate anywhere in your stack.
{% endhint %}

![Note the 3-stack of review\_queue\_api, review\_queue\_server, and review\_queue\_frontend](<../../.gitbook/assets/Screen Shot 2021-10-14 at 11.53.30 AM.png>)

## Checking out a branch

Branches in Graphite are just git branches under the hood - you can check them out with native git, but the easiest way is to use `gt branch checkout`:

```bash
# checkout review_queue_server
gt branch checkout tr-PK31--review_queue_server
```

If you aren't sure which branch you want to checkout, you can also use `gt branch checkout` in interactive mode:

![gt branch checkout (interactive mode)](<../../.gitbook/assets/Screen Shot 2022-05-04 at 11.23.21.png>)

Now, if you run `gt log` you'll be on `review_queue_server` as intended:

![](<../../.gitbook/assets/Screen Shot 2021-10-14 at 4.06.09 PM.png>)

## Moving up and down a stack

{% hint style="info" %}
**Upstack**: branches further away from `main` in a stack (more recent)

**Downstack**: branches closer to `main` in a stack (less recent)
{% endhint %}

Sometimes you want to move to the branch directly above or below the current branch in a stack. Graphite's CLI makes this easy:

```bash
# check out the branch directly up-stack (in this case review_queue_frontend)
gt branch up

# check out the branch directly down-stack (in this case back to review_queue_server)
gt branch down

# move multiple branches at a time (back to main)
gt branch down 2
as
# move multiple branches at a time (back to review_queue_frontend)
gt branch up 4

# move to the base of the stack, not including main (to review_queue_api)
gt branch bottom

# move to the tip of the stack (back to review_queue_frontend)
gt branch top
```

{% hint style="info" %}
If you find yourself navigating a stack which splits into smaller stacks, `gt branch up` and `gt branch top` will ask which child branch you'd like to checkout if there's ever ambiguity.
{% endhint %}

Now that you can quickly navigate your stack, let's take a look at how you can easily update branches mid-stack.
