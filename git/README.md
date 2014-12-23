# Git

This is the guide to rule every project with version control.

* Write meaningful commit messages, don't just go simple and short
* Start your commit message with a present verb such as `Adds`, `Removes`, `Updates`
* Squash multiple commits
* Avoid merge commits. Use a rebase workflow
* Delete local and remote branches after merge has been done
* Every new feature should be build on a separate branch
* Never track files specific to your local development machine.

## Set up the laptop

You can easily set up your laptop by running [kaishi](https://github.com/IcaliaLabs/kaishi), a shell script to convert any Mac OS X or Linux computer into a real development machine. This will install the latest version of git.

## Branch structure

We at [Icalia Labs](http://icalialabs.com) never work directly on the `master` branch to build software, we like to keep things isolated. And although we make a branch per feature, but we consider an extra branch called `dev` where we mantain all of the source code HEAD, so `dev` always reflect the most recent changes to be released.

Once the `dev` branch is stable enough we then merge with `master` and tagged with a version number. This way we keep things sane and the CI server can easily push to production or rollback to the last stable version on production.

An image is presented below to demostrate this:

![http://nvie.com/posts/a-successful-git-branching-model](http://nvie.com/img/main-branches@2x.png)


## Write a new feature

Now that we understand how the `dev/master` flow works, it is time to get to know how to start a new feature.

First create a local feature branch off `dev`:

```console
$ git pull origin dev
$ git checkout -b <feature-branch>
```

In the branch creation it is important that you prefix the name of it with your initials.

Once you are done with the feature it is time to merge it with `dev`, but first we need to fetch for changes

```console
$ git fetch origin
```

If there are changes in the upstream you should rebase them and squash them to make them more atomic:

```console
$ git rebase -i origin/dev
```

Resolve every conflicts, and make sure the tests are passing:

```console
$ git add --all
```

Once the `dev` branch is up to date, it is time to merge your feature branch.

```console
$ git checkout dev
$ git merge <feature-branch>
```

Share and delete your branch:

```console
$ git push origin <feature-branch>
$ git branch --delete <feature-branch>
```

**If you think that you might need some code review from another developer, you can ask him/her kindly, and place a pull request assigned to him/her**


## .gitignore samples

* [Rails]()
* [iOS]()