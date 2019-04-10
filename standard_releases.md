# Standard Releases

The Standard is given release numbers.

These are applied in the repository https://github.com/openownership/data-standard

Each release is a branch (NOT a tag), for example:

  *  https://github.com/openownership/data-standard/tree/v0-0-3
  *  https://github.com/openownership/data-standard/tree/v0-1

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
