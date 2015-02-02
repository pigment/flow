The following process is based on [GitHub flow](http://scottchacon.com/2011/08/31/github-flow.html). You may also find this [article on rebasing pull requests](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request) useful, as well as [GitHub's tips for writing a good pull request](https://github.com/blog/1943-how-to-write-the-perfect-pull-request).

It assumes that a remote automated testing service (e.g. https://circleci.com) has been integrated with GitHub.

## Getting Started

The main idea is that the master branch should always be deployable. All work should be done on separate branches and merged in.

So for any bit of work you do, create a branch (usually off master) with a descriptive name:

    $ git checkout master
    $ git checkout -b my-descriptive-branch-name

Make changes and commit to this branch, and push to a remote branch regularly (this will run the tests remotely):

    $ git commit -m "A description of the changes"
    $ git push origin my-descriptive-branch-name

## Making pull requests

When you need feedback or help, or you think your branch is ready for merging, open a pull request. The easiest way to do this is via the pull request tab on the project page. From there, choose the your branch in the "compare" dropdown, or pick it from the "Example Comparisons" list.

See [GitHub's tips for creating and handling pull request discussions](https://github.com/blog/1943-how-to-write-the-perfect-pull-request).

## Signing Off, Merging, & Deploying

If tests pass and you feel that the branch is ready for merging, ask for sign off from another member of the team, @mentioning members if necessary. (Guidance for reviewing pull requests can be found in Appendix B: Reviewing pull requests.)

After approval, you can merge it into master. This is usually just a case of pressing the "Merge pull request" button on the pull request page. (If the pull request cannot be merged automatically, checkout the rebasing steps below.)

Delete your branch if necessary. This is easily done on the GitHub site.

After merging on GitHub, **ensure your local master branch is up-to-date** by running:

    $ git checkout master
    $ git pull origin master

Then deploy, and give yourself a pat on the back!

## What about small stuff that doesn't need to be reviewed and signed off?

There may be the odd occasion where a change will not need to be reviewed, and you need to deploy an urgent fix. The same processed should be followed, but the review step can be omitted.

## Pull Requests that Cannot be Merged Automatically

In some cases a pull request will have merge conflicts and won't be able to be merged automatically. The following steps should help.

Make sure your branch itself is up-to-date with master:

    $ git fetch
    $ git checkout my-descriptive-branch-name
    $ git rebase origin/master

… fix any conflicts, then force push to your branch:

    $ git push -f origin my-descriptive-branch-name

Return to the pull request on GitHub to merge using the "Merge pull request" button.

## Appendix A: Why?

We want the business to _maximise the value from the work we've invested in_. Customers start benefitting sooner if _changes are deployed without breaking anything, and as soon as they are ready._

Deploying a change is one of the riskier things we do. _We have the potential of damaging the relationship with customers, and interrupting the work of our team._ To reduce this risk, ownership of a change is important. The developer who worked on the change should be the person who is ultimately responsible to merge the change and make the change live. They should follow it through to production, and look out for any errors that were not found during test runs. Developers may want to schedule more complicated changes for a time when they can fix any unexpected problems that may arise.

When different developers are working on different patches and projects, the timeline of a change becomes important. _If someone is working on an important or urgent fix, they shouldn't be forced to make another team member's change live (risky) in order to deploy their fix._ There should be a stable timeline to make changes live, that minimises the risk of blocking another team member's work (or forcing them to risk deploying something they have no knowledge of).

For this to work, we all need to be on board with a common process. _We've worked together to choose the most light-weight process that fits our needs_. Any suggestions or improvements are welcome.

## Appendix B: Reviewing pull requests

You aren't expected to fully understand a pull request, and you are not taking responsibility for it. Some of the benefits might be:

* It encourages the author to code more responsibly if they know a colleague is going to intentionally look at it
* It increases team cohesion (people know what's going on)
* It distributes knowledge more widely (more people know at least a bit about more systems)
* We can learn from one another (you might spot an interesting approach or pattern)
* It gives others the opportunity to give another perspective to the problem, potentially improving the feature or solution

If you have been asked to review a pull request, here are some of the things you can do:

* Ask high level questions of anything you don't understand (or look in the associated ticket)
* Take a look at the code style and see if there is anything you can learn, ask questions
* Look out for typos in copy, variable names, methods
* If it's a bug fix or behaviour change, see if there are associated tests and if not, ask why not

Importantly:

* You don't need to test it (this may change in future, but for now it would be too much work)
