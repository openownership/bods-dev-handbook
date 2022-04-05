# Git Branches, Version Numbers and Standard Releases

## Contents

* [Overview](#overview)
* [Versioning](#versioning)
* [Translations and releases](#translations-and-releases)
* [Release processes](#release-processes)
  * [A new release](#a-new-release)
  * [A new language to the current release](#a-new-language-to-the-current-release)
  * [Fixes to an existing release](#fixes-to-an-existing-release)
  * [Fixes to an existing translation](#fixes-to-an-existing-translation)
  * [Non-material changes](#non-material-changes)


## Overview

Development is normally done on the `master` branch. All released versions of the
standard live in other, specially named, release branches (**not tags**).

By default, new work should happen on a branch taken from the master branch and
be merged back into master, via a pull request, as soon as possible. However, in
some cases you may need to branch from a specific release branch and merge
your changes back into that release branch. It's best to discuss this before
making changes if you're unsure.

Note that the default, merging into master, does not release any changes to the
world immediately. Changes in master will be incorporated into the next release
of the standard, which may be some time. If your changes affect the current, or
older, versions they must be released by bringing the changes into those
respective release branches. This can introduce complications, so again is best
confirmed ahead of time.

## Versioning

The Standard is given release numbers, following roughly the principles of
[Semantic Versioning](https://semver.org/), where each part of a version number
has significance to users and is used by them to understand the differences
between versions.

These version numbers are applied in the main BODS repository
[github.com/openownership/data-standard](https://github.com/openownership/data-standard)
as a naming convention for release branches, for example:

* [github.com/openownership/data-standard/tree/0.0.3](https://github.com/openownership/data-standard/tree/0.0.3)
* [github.com/openownership/data-standard/tree/0.1.0](https://github.com/openownership/data-standard/tree/0.1.0)

These releases are published by enabling the release branch in ReadTheDocs, the
"latest" tag in ReadTheDocs is manually changed to point at the latest version.

**Note:** our release branch naming scheme is "MAJOR.MINOR.PATCH"

**Note:** we always include trailing zeroes in our version numbers. e.g. "0.1.0" is
preferred over "0.1" because someone might interpret the latter as the latest
version of v0.1

## Changelog
A [changelog](https://github.com/openownership/data-standard/blob/master/docs/schema/changelog.rst) is kept of changes to the schema and documentation. Before a PR is merged into
the `master` branch, you should consider whether an update to the changelog is
necessary. (Broadly: is this a change that will materially effect people's use
of BODS? Fixing a typo: no, not necessary. Editing a schema property's
description for clarity: possibly necessary.) If there is no specific BODS
release planned, but material changes need to be noted in the changelog, items
can be added under a `## [Unreleased]` heading.

See https://keepachangelog.com/en/0.3.0/ for more on maintaining a good changelog.

## Translations and releases

New releases for the standard must be translated into supported languages.

For incremental work on the schema and documentation, translations do not need
to be complete before changes are merged into the main branch. Translation
may happen periodically during work on a new version, but it is usually better
to wait until a stable version is ready and then translated all at once, just
prior to a versioned release. This reduces the risk of translators working on
text that may change again in the near future.

## Release processes

How exactly we perform a release depends on what is being released and which
versions the changes affect. The sections below detail specific scenarios, but
the following general questions always apply:

1. Has the schema or any normative documentation changed?
2. Does text need translating?
3. Do the changes affect any existing, released versions?

### A new release

Preparing a new release is the most straightforward scenario, though not the
least work! The general process is:

* Decide on the set of changes that will be released. Some of these will have
  likely already been merged in the course of normal development, but they may
  need additional development, examples adding, etc.
* Review, test and merge those changes into the `master` branch.
* Call a "freeze" on the `master` branch. This freeze lasts during the translation
  process and applies to the schema and docs folders in the repository.
* Begin translation of the new release (see [translations](/translations)) using the
  BODS-main project in Transifex.
* During translation there may be a need to fix issues that exist on the `master`
  branch. If they are outside schema and docs they can be developed on a branch
  taken from `master` and merged back in when completed.
  If the changes affect schema and/or docs then they may, in turn, affect the
  translation. The process for making these changes is:
  * First create an issue in Github to track the problem.
  * Then create a new branch that uses the issue number, eg.
    `297-concept-translation`.
  * When the branch is ready to be merged into `master`, ensure that the translations
    on the new branch are either equivalent to or ahead of the translations on
    `master`. ie. if no new translations have been merged back into `master` since the
    new branch was made, no need to pull new translations down from Transifex. But if
    `master` has since been updated, be sure to fetch the new translations to the new
    branch, either from Transifex or by rebasing against `master` (the best option will
    depend on the changes you have made in the new branch).
  * Merge the branch (`297-concept-translation`) into `master`.
  * Checkout the `master` branch, extract the new or changed strings per the translation
    process, and push them up to Transifex.
  * Wait for the new changes to be translated.
  * Once the translation is finalised, check out a new branch for the translations and
    pull them from Transifex. Commit these and make a PR against `master` to bring it up
    to date.
* Once the release is finalised and everything is ready, create a branch for the
  new version (eg, `0.2.0`) from `master`.
* [Create a new Transifex project](translations.md#creating-and-configuring-a-new-project-in-transifex)
  named for the new version (eg. `bods-v02`).
* Configure the Transifex config on the versioned branch with the versioned Transifex
  project (and commit this), and push both the source files *and* the translations
  to the new Transifex project. This means that further work on the schema and
  documentation *and* the equivalent translations can proceed on the `master` branch
  and in the `BODS-main` Transifex project, while the versioned release remains fixed.
* Make the new version live on ReadTheDocs.

### A new language to the current release

Until such time that we support several stable releases, our assumption is that
only the current release (and any future ones) will be translated into new
languages.

The current release has its own project in Transifex, for example BODS 0.2.0
has an equivalent `bods-v02` Transifex project. New languages for translation
can be added at any time through the Transifex UI.

The new language should also be added to the `BODS-main` Transifex project,
as well as the [Sphinx theme](https://github.com/openownership/data-standard-sphinx-theme).

If the `master` branch and the current stable release have not diverged
significantly:

* Make a new translation branch from the release branch, (e.g. `0.2.0`) for the
  translation work (e.g. `0.2.0-esperanto-translation`). 
  * Remember also that there are translations in the
    [theme repo](https://github.com/openownership/data-standard-sphinx-theme), and
    the pinned commit of that package needs to be updated in `requirements.txt`
    to bring those in.
* Pull the new translations from Transifex, commit them, and merge the branch
  into the versioned branch (`0.2.0`).
* Make a new branch from `master` (eg. `esperanto-translation`) and bring
  across the changes from your translation branch. `git cherry-pick` is
  usually easiest.
* Double check there are no new translations in `BODS-main` that were not present
  in the versioned branch. Then push your local translations up to Transifex
  (`tx push -t`; you may need to use `--force` but in theory Transifex should
  be happy that your local translations are the newest and let you push them).
* Make the new language live on Read The Docs (see [translations](/translations))

When `master` and the current release have diverged significantly, treat
the translation of each as a separate project. Translate the versioned release
as described above. Translate `master` only when it is due for release, or at
the next point in the development process that makes the most sense.

### Fixes to an existing release

When a bug is discovered or a correction needs to be made to an existing
release and it is deemed severe enough to require an immediate fix (i.e.
it cannot wait for the next naturally-occurring release), then we need
to make an unplanned release. The process for this is as follows:

* Make an issue in the data-standard repo describing the problem
* Make a new branch named after the issue, i.e. `1234-description-of-issue`
  from the current release branch and commit the fix(es) to it
* Review and test this branch in a pull-request
* If necessary, perform necessary translation work on this branch once this fix
  is approved in English. Whether this is necessary depends on the nature of the
  fix, i.e. whether it changes translated text. Be sure to use the correct
  Transifex project for the version being updated.
* At this point, we need to decide on the impact of the changes on users of the
  standard and the appropriate new version number. Create a new release branch
  named accordingly, e.g. `0.2.1` or `0.3.0` and merge the fixes into it.
* Follow the usual release process of enabling, updating to latest, etc, so that
  this release becomes the new 'current' release. If the issue warrants it,
  consider adding a notice to the old release documenting the issue and that it
  should not be used. You may also have to notify existing users of that
  version.
* If the fixed issue is also present in `master`, the fix branch should also be
  merged back into there, in a separate pull-request.

**Note:** until we hit a stable 1.0 release, only very severe bugs that impede real
world use of the standard, present a security risk or otherwise cause significant
damage to our aims as an organisation should require this kind of fix. It is also
assumed that other older pre 1.0 releases are automatically and immediately
considered end-of-life when a new version is released. This policy is likely to
change only when we have real world use or commitments mandating a greater level
of support.

### Fixes to an existing translation

Fixes that solely relate to an existing translation (i.e. not the source text,
but a particular translation of it) should follow a similar process to other
fixes to an exiting release. The fix can be made by editing the translation
in Transifex and pulling down the updated strings to a local branch named for
the issue eg `297-concept-translation`. This should then be pushed up and merged
directly back into the existing release branch.

This sort of fix does not require a change in version number or a new release
branch.

### Non-material changes

Changes which do not affect the standard, or normative documentation accompanying
it, do not need a corresponding change in version number. However, it's still
important to consider whether any text has been added or changed, and which
existing versions of the standard you wish the changes to appear in.

**Examples:**

- Making a change to the visual style of the standard website such as
  [data-standard-sphinx-theme#57](https://github.com/openownership/data-standard-sphinx-theme/pull/57)
  requires both the translation of a new piece of text and the merging of the
  updated theme into all the existing released versions of the standard. Note
  this also needed updates to the theme and a new pinned version.
- Adding additional language examples to a released version
  [data-standard#260](https://github.com/openownership/data-standard/pull/260)
  which can be merged into `master` **and** the current release.
- Updating an underlying software library
  [data-standard#291](https://github.com/openownership/data-standard/pull/291)
  which can be merged directly into `master` and does not need to update any
  current or previous versions.

In general, the process for these kinds of changes should be:

* Do the work on a branch based on the master branch, pull-request & approve it,
  merge it back into `master`
* For each old release we want to put the work on, create a new branch from that
  version, `git cherry-pick` or `git merge` the commits across, resolve any
  conflicts, pull-request and finally merge into that version.
* If textual changes are made, each branch being merged into existing versions
  should also consider the translations needed and when/how they will be
  performed. As with other fixes, the most important is the current release,
  which should not suffer degradation of translation quality for long/at all if
  possible. Other, older branches should be evaluated on a best-effort basis.

**Note:** particularly important files which *must* be synced across all releases
are:
* LICENSE
* docs/about (particularly licensing and privacy info)
