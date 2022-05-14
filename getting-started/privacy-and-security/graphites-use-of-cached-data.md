# Graphite's use of cached data

At the moment, Graphite caches three types of data in our database:

* **Personal data**: For example, user avatar image,  user name, user email. These are fields used throughout our website that we don't want to have to re-query GitHub for every time.&#x20;
* **Org membership**: For example, Tomas is a member of the Graphite org. We pretty much exclusively use this information for analytics purposes (How many users do we currently have at Graphite? For users at Graphite, what is their average load time?)
* **PR metadata**: Specifically,
  * Title
  * Description
  * Author
  * Number of lines added / removed
  * Branch name and name of branch you're merging in to (we use this to construct the stack)
  * Is merged
  * Is closed
  * Reviewers (and associated status: approved, request changes, etc.)
  * CI rollup status (passing, failing, etc.)
  * Along with a handful of timestamps (created at, updated at., etc.)

Originally we didn't store this information, now we cache it to provide you a faster experience (it's hard to load a list of 100 PRs in your review queue if we need to fetch the metadata for those PRs individually).&#x20;



**We do not cache any code** (we understand that's sensitive), and if that's a concern, happy to find a way to guarantee that to you (for instance, through a signed agreement or some portal to let you audit what data we store on your behalf). When you load the PR page, we query for all of that data in the moment. You can think of us as a very fancy GitHub client. \
