# Navigating a stack

#### Let's say this is the state of your repo - Graphite makes it easy to navigate!

![](<../../.gitbook/assets/image (7).png>)

## Checking out a branch

Branches in Graphite are just git branches under the hood - you can check them out with native git, but the easiest way is to use `gt branch checkout`:

```bash
# checkout review_queue_server
gt branch checkout jg--06-14-part_1
```

If you aren't sure which branch you want to checkout, you can also use `gt branch checkout` in interactive mode:

![](<../../.gitbook/assets/image (23).png>)

Now, you can see in `gt log short` you're on `part_1` as intended:

![](<../../.gitbook/assets/image (18).png>)

## Moving up and down a stack

{% hint style="info" %}
**Upstack**: branches further away from `main` in a stack (more recent)

**Downstack**: branches closer to `main` in a stack (less recent)
{% endhint %}

Sometimes you want to move to the branch directly above or below the current branch in a stack. Graphite's CLI makes this easy:

```bash
# check out the branch directly up-stack (in this case part_2)
gt branch up

# check out the branch directly down-stack (in this case back to part_1)
gt branch down

# move multiple branches at a time (up to part_3)
gt branch up 2

# move multiple branches at a time (back to main)
gt branch down 3

# move to the tip of the stack (back to part_3)
gt branch top

# move to the base of the stack, not including main (to part_1)
gt branch bottom
```

{% hint style="info" %}
If you find yourself navigating a stack which splits into smaller stacks, `gt branch up` and `gt branch top` will ask which child branch you'd like to checkout if there's ever ambiguity.
{% endhint %}

Now that you're comfortable with the basics of creating a stack and navigating around it, let's submit your changes!
