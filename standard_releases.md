# Versioning and Releases

## Contents

* [Overview](#overview)
* [Versioning](#versioning)
* [Normative vs non-normative changes](#normative-vs-non-normative-changes)
* [Changelog](#changelog)
* [Translations and releases](#translations-and-releases)
* [Release processes](#release-processes)
  * [A new release](#a-new-release)
  * [Adding a new language to the current release](#adding-a-new-language-to-the-current-release)
  * [Making fixes to an existing release](#making-fixes-to-an-existing-release)
  * [Making fixes to an existing translation](#making-fixes-to-an-existing-translation)
  * [Making non-normative changes](#making-non-normative-changes)
* [Freeze checklist](#freeze-checklist)


## Overview

Development is normally done on the `main` branch. All released versions of the
standard are in specially named release branches (**not tags**).

New work should happen on a branch taken from the main branch and
be merged back into main, via a pull request, as soon as possible. However, in
some cases you may need to branch from a specific release branch and merge
your changes back into that release branch. It's best to discuss this before
making changes if you're unsure.

Note that the default, merging into main, does not release any changes immediately. Changes in main will be incorporated into the next release
of the standard, which may be some time later. If your changes affect the current, or
older, versions they must be released by bringing the changes into those
respective release branches. This can introduce complications, so is best
discussed ahead of time.

## Versioning

A new release is only required for normative changes to the standard. Once BODS reaches version 1, releases will follow the principles of [Semantic Versioning](https://semver.org/).  

This distinguishes between:
* MAJOR version releases, which make backwards-incompatible changes (e.g. from 1.2.0 to 2.0.0)
* MINOR version releases, which add functionality in a backwards-compatible manner (e.g. from  1.1.0 to 1.2.0)
* PATCH version releases, which make backwards-compatible bugfixes (e.g. from 2.0.0 to 2.0.1)

If a change is backwards-compatible, this means that data shared using the earlier version of the standard will still meet the requirements of the latest version. (e.g. data shared in 1.0.0 format will also comply with the requirements for version 1.1.0 or 1.0.1) 

Before a version 1 release of BODS, backwards-compatibility between minor releases is not guaranteed.

Version numbers are applied in the main BODS repository
[github.com/openownership/data-standard](https://github.com/openownership/data-standard)
as a naming convention for release branches, for example:

* [github.com/openownership/data-standard/tree/0.0.3](https://github.com/openownership/data-standard/tree/0.0.3)
* [github.com/openownership/data-standard/tree/0.1.0](https://github.com/openownership/data-standard/tree/0.1.0)

These releases are published by enabling the release branch in ReadTheDocs, the
"latest" tag in ReadTheDocs is manually changed to point at the latest version.

**Note:** we always include trailing zeroes in our version numbers. e.g. "0.1.0" is
preferred over "0.1" because someone might interpret the latter as the latest
version of v0.1

## Normative vs non-normative changes 

Non-normative changes, which do not require a new release, include:
* Changes to the Homepage, Primer, Example Data or About pages (in the repo /docs folder)
* Typo corrections on any documentation page (in the repo /docs folder)
* The addition of new example data (in the repo /examples folder) 
* Changes to the readme
* Updates to dependencies (requirements.txt or requirements_test.txt) 
* Changes to readthedocs templates 
* Addition of a new translation
* Changes to the automated tests 

Normative changes, which do require a new release, include:
* Any changes to the BODS JSON schema (repo /schema folder)
* Any changes to tests and test data (repo /tests folder)
* Changes to the Data Standard pages (repo /docs/standard folder)
* Changes to the License

## Changelog
A [changelog](https://github.com/openownership/data-standard/blob/master/docs/schema/changelog.rst) is kept of changes to the schema and documentation. Before a PR is merged into
the `main` branch, you should consider whether an update to the changelog is
necessary. (Broadly: is this a change that will materially effect people's use
of BODS? Fixing a typo: no, not necessary. Editing a schema property's
description for clarity: possibly necessary.) If there is no specific BODS
release planned, but material changes need to be noted in the changelog, items
can be added under an `## [Unreleased]` heading.

See https://keepachangelog.com/en/0.3.0/ for more on maintaining a good changelog.

## Translations and releases

New releases for the standard must be translated into supported languages.

For incremental work on the schema and documentation, translations do not need
to be complete before changes are merged into the main branch. Translation
may happen periodically during work on a new version, but it is usually better
to wait until a stable version is ready and then translate all at once, just
prior to a versioned release. This reduces the risk of translators working on
text that may change again in the near future.

## Release processes

How we perform a release depends on what is being released and which
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
* Review, test and merge those changes into the `main` branch.
* Go through the [Freeze checklist](#freeze-checklist) (below) and ensure that all elements of the docs and schema have been updated and tested as outlined.
* Call a "development freeze" on the main branch. This freeze lasts during the translation process and applies to the schema and docs folders in the repository.
    * See below for how to make necessary edits during a "freeze".
* Carry out translation of the new release (see [translations](/translations)) using the
  BODS-main project in Transifex. The final step of this is to
  pull completed translations from Transifex and merge them into `main`.
* Create a branch for the new version (e.g. `0.5.0`) from `main`.
* [Create and configure a new Transifex project](translations.md#creating-and-configuring-a-new-project-in-transifex)
  named for the new version (e.g. `bods-v05`). Remember to commit the changes
  you make to the Transifex config to your versioned branch (`0.5.0`). This means that
  further work on the schema and documentation *and* the equivalent
  translations can proceed on the `main` branch and in the `BODS-main`
  Transifex project, while the versioned release remains fixed.
* Make the new release live on ReadTheDocs:
  1. On the Versions page of the main ReadTheDocs project, make the new version branch active and not hidden. (If the new branch doesn't appear in the 'Activate a version' list, you will need to build an existing branch so that ReadTheDocs notices the new branch.) 
  2. In Admin > Advanced Settings, set the 'Default version' and 'Default branch' to the new version branch.
  3. On the Builds page, build both the new version branch and 'latest'. 
  4. Carry out steps i - iii for all related translation projects in ReadTheDocs.
  5. On the live site, test the new version and language switching for all translations.
* Consider which BODS-handling tools will now need to be updated. (Add interim banners to such tools with a message like: "This tool is currently being updated to handle BODS x.x data".)

#### Editing during a "freeze"

During translation, there may be a need to fix issues that exist on the `main`
branch. If they do not affect anything that needs to be translated (docs,
schema, codelists) they can be developed on a branch taken from `main` and
merged back in when completed.
  
If the changes affect schema and/or docs then they may, in turn, affect the
translation. The process for making these changes is:

* First, create an issue in GitHub to track the problem.
* Then create a new branch that uses the issue number, e.g. `297-fix-typo` and
  make the needed changes.
* Determine if any of the strings you have changed have *already been
  translated* in Transifex. If so, advise the translators of the nature of the
  change you made to the English string. Even small changes, like fixing
  spelling, punctuation or markup can cause Transifex to detect a new source
  string and reset the translation. If the change is small, the translators
  can reuse what they had before (with punctuation/markup fixes as applicable).
  If the change is large (e.g. a complete sentence rewrite), they probably need
  to translate it again from scratch. Agree when you are going to push the
  updated string to Transifex, and proceed with the following steps at that time.
* After review, merge the branch (`297-fix-typo`) into `main`.
* Checkout the `main` branch and follow
  [the translation process](https://github.com/openownership/data-standard/blob/master/README.md#managing-the-translation-workflow)
  so that the new or changed strings are extracted, and push them to Transifex.

### Adding a new language to the current release

Until such time that we support several stable releases, our assumption is that
only the current release (and any future ones) will be translated into new
languages.

The current release has its own project in Transifex, for example BODS 0.2.0
has an equivalent `bods-v02` Transifex project. New languages for translation
can be added at any time through the Transifex UI.

The new language should also be added to the `BODS-main` Transifex project,
as well as the [Sphinx theme](https://github.com/openownership/data-standard-sphinx-theme).

If the `main` branch and the current stable release have not diverged
significantly:

* Make a new translation branch from the release branch, (e.g. `0.2.0`) for the
  translation work (e.g. `0.2.0-esperanto-translation`). 
  * Remember also that there are translations in the
    [theme repo](https://github.com/openownership/data-standard-sphinx-theme), and
    the pinned commit of that package needs to be updated in `requirements.txt`
    to bring those in.
* Pull the new translations from Transifex, commit them, and merge the branch
  into the versioned branch (`0.2.0`).
* Make a new branch from `main` (e.g. `esperanto-translation`) and bring
  across the changes from your translation branch. `git cherry-pick` is
  usually easiest.
* Double check there are no new translations in `BODS-main` that were not present
  in the versioned branch. Then push your local translations up to Transifex
  (`tx push -t`; you may need to use `--force` but in theory, Transifex should
  detect that your local translations are the newest and let you push them).
* Make the new language live on Read The Docs (see [translations](/translations))

When `main` and the current release have diverged significantly, treat
the translation of each as a separate project. Translate the versioned release
as described above. Translate `main` only when it is due for release, or at
the next point in the development process that makes the most sense.

### Making fixes to an existing release

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
* If the fixed issue is also present in `main`, the fix branch should also be
  merged back into there, in a separate pull-request.

**Note:** until we hit a stable 1.0 release, only very severe bugs that impede real
world use of the standard, present a security risk or otherwise cause significant
damage to our aims as an organisation should require this kind of fix. It is also
assumed that other older pre 1.0 releases are automatically and immediately
considered end-of-life when a new version is released. This policy is likely to
change only when we have real world use or commitments mandating a greater level
of support.

### Making fixes to an existing translation

Fixes that solely relate to an existing translation (i.e. not the source text,
but a particular translation of it) should follow a similar process to other
fixes to an existing release. The fix can be made by editing the translation
in Transifex and pulling down the updated strings to a local branch named for
the issue eg `297-concept-translation`. This should then be pushed up and merged
directly back into the existing release branch.

This sort of fix does not require a change in version number or a new release
branch.

### Making non-normative changes

In general, the process for these kinds of changes should be:

* Do the work on a branch based on the main branch, pull-request & approve it,
  merge it back into `main`
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

## Freeze checklist

1. Ensure that all pages in the docs/about/ directory have been reviewed and updated if necessary.
2. Update the license file (root of repo).
3. Update the ReadMe file (root of repo).
4. Check docs/schema/reference.rst. Are all new objects, properties and codelists there? Have sub-properties been collapsed sensibly?
5. Update BODS version ‘attention’ box on all relevant docs pages
6. Do a final edit of docs/schema/changelog.rst
7. Fix any sphinx build warnings or errors (including broken links)
8. Update all example and test BODS json data to increment `bodsVersion` value. (And 'bodsVersionTypo' in one test file.)
9. Update the `version` field value in all schema .json files
10. Update the two version references in index.rst (home page of the docs).
11. Update docs/conf.py and check the docs build without errors.
12. Run pytest finally, and resolve any errors.
