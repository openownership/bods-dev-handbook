# Git Branches, Version Numbers and Standard Releases


## Normal Standard Development

All development is done on the "master" branch.

When doing work, a branch should be taken from the master branch. The branch name should start with the number of the issue, for example "136-use-externallinks".

Branches should be a self contained piece of work, and merged back to "master" as soon as possible. 
The longer branches exist, the harder it can be to merge them back as the possibilities of there being merge conflicts increases.

Branches should be merged back to "master" as soon as possible via a pull request. A review is needed.

### Freezes on the "master" branch

When the "master" branch is almost ready to be released, a "freeze" may be declared for certain types of content.

eg As the Russian translation is being done, no pull requests that change the content of strings on the site would be allowed.

In these cases code reviewers should be informed of the "freeze" and they can enforce the freeze whilst reviewing pull requests - some pull requests may be put on hold for a while.

### Working on the release after the next release

This means that anything on the master branch will be included in the next release.

If you are working on things for the release after the next release these can not be merged to master yet.
For example, if 0.1 is the current release, 0.2 is the next release and 0.3 the release after, only work for 0.2 should be merged to master.

## Versioned Releases

The Standard is given release numbers.

These are applied in the repository [github.com/openownership/data-standard](https://github.com/openownership/data-standard)

Each release is a branch (NOT a tag), for example:

  *  [github.com/openownership/data-standard/tree/v0-0-3](https://github.com/openownership/data-standard/tree/v0-0-3)
  *  [github.com/openownership/data-standard/tree/v0-1](https://github.com/openownership/data-standard/tree/v0-1)

That branch is then enabled in ReadTheDocs and the "latest" tag in ReadTheDocs is changed to be the new version.

## To make a new release

* Make sure the master branch is fully ready, with updated version numbers and so on. (TODO expand this?)
* Create a new branch from the master with the naming scheme "vX-Y-Z", (eg "v0-0-3" or "v0-1-0". Note the included zero in the last example - that does conflict with a previous branch but should be used in the future)
* Enable the branch in ReadTheDocs
* Switch the latest tag in ReadTheDocs to the new branch

Note: "v0-1-0" is preferred over "v0-1" because someone might interpret the latter as "The latest version of the v0.1 spec, eg v0.1.5 or something" and so "v0-1-0" is preferred to make clear which version it is.

## Releasing non-schema or non-documentation code that gets done after a release

Each release of the standard is a separate branch (NOT a tag) in git. This means that any non-schema or non-documentation code that we need to do to make ReadTheDocs work, or something like that, can be added easily. The process would be:

  *  Do the work on the master branch, approve it, merge it in. It's done for the future.
  *  For each old release we want to put the work on, switch to that branch, "git cherry-pick" the commits across, resolve any conflicts, test it, push to github.

This is a manual process, but hopefully one that's easy to do.
