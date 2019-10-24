# Translations

The processes, roles and mechanisms detailed below implement the [BODS Language Support Policy](https://docs.google.com/document/d/1E15uIOO_JRU2_hFvetaMu4L66hJSrJMuK1U0lenDiyA).

Note: This process is still in development, and improvements or clarifications are welcome.

The following instructions cover the translation of:

  * A version of the Beneficial Ownership Data Standard (BODS) schema, including its codelists
  * The corresponding documentation website 
  * The documentation website’s theme

## Locations of source files to be translated

BODS **schema** and **codelists** exist under the [schema folder within the BODS Github repository](https://github.com/openownership/data-standard/tree/master/schema).
The content for the BODS **documentation** website exists under the [docs folder within the same BODS Github repository](https://github.com/openownership/data-standard/tree/master/schema).
The documentation website’s **theme** has its own Github repository - [data-standard-sphinx-theme](https://github.com/openownership/data-standard-sphinx-theme).

By translating the three components listed above the publicly available website at http://standard.openownership.org can be published in translation. This is the aim of the translation work.

## Scope of translation work

Things that are in scope for translation are:

  * All prose in the **documentation**.
  * Text like menu items and footers in the **documentation theme**.
  * The *values* of **schema** fields `title` and `description`.
  * The *values* of **codelist** fields `title`, `description` and `technical note`.
  * The SVG diagrams in the **documentation**.

Things that need to become part of the translation workflow but are not yet:

  * The example data in the [data-standard repo](https://github.com/openownership/data-standard).

## Overview of the translation workflow

The workflow for doing the translation is:

  * extract the strings that need to be translated from the repositories 
  * push the strings up to their Transifex project 
  * have the strings translated, reviewed and proofread 
  * pull the translated strings down from Transifex 
  * upload them to their respective repositories and 
  * make them live on the website.

The diagram below provides an extremely high-level overview of the workflow. It excludes the final step of making the translation live.

![Translation Workflow](https://github.com/openownership/bods-dev-handbook/blob/master/screenshots/translation/translation_workflow_overview.png)

## Setting up your local machine

Complete the following steps to get your system set up to undergo the workflow outlined above (assumes Ubuntu 18.04.2 LTS or similar):

  * set up an account and join the ODSC organization in Transifex
  * create and configuring a new project in Transifex
  * clone the repositories to manage the workflow 
  * install and configure the Transifex client

### Setting up an account and joining the ODSC organization in Transifex

Create a free Transifex account on their [sign up page](https://www.transifex.com/signup/).

The organization is the home of all the translation projects that an organization runs on Transifex.

Open Data Services Co-operative is already set up as an organization in Transifex and all of our projects and teams are managed from within it. A list of our translation projects is visible at the [Open Data Services Co-operative public page](https://www.transifex.com/OpenDataServices/public/).

![ODSC Organisation in Transifex](https://github.com/openownership/bods-dev-handbook/blob/master/screenshots/translation/transifex_odsc_organisation.png)

Once you have signed up to Transifex you should ask an administrator of ODSC to make you an administrator too. We don't maintain a list of those administrators here, but there is a considerable overlap with the [people who contribute towards the BODS Standard repository](https://github.com/openownership/data-standard/graphs/contributors).

### Creating and configuring a new project in Transifex

  * [Add a new project on Transifex](https://www.transifex.com/OpenDataServices/add/).
  * Name it according to the version of BODS, ie `bods-v02` for BODS version 0.2.
  * Choose 'public project' and **make sure to check the 'My project is a non-commercial Open Source project checkbox'** and enter the github repo URL.
  * ![Screenshot: tick the My project is a non-commercial Open Source project checkbox when creating a new project](screenshots/translation/transifex_noncommercial.png)
  * Assign the project to the BODS team.
  
TO DO: Decide upon and document a policy for using (or not) the Translation Memory functionality.

### Cloning the repositories to manage the workflow

Follow the instructions in the [BODS data-standard-sphinx-theme README.md](https://github.com/openownership/data-standard-sphinx-theme).

### Installing and configuring the Transifex client

#### Installing the Transifex client

Transifex offers a number of different options for uploading content to be translated. In this documentation we will describe the process for setting up the Command Line Interface (CLI) Client. 

The commands for installing the Transifex CLI client on Ubuntu are:

```
$ sudo apt-get install python-pip
$ sudo pip install transifex-client
```

#### Configuring the Transifex client

Transifex configuration involves the creation of two files:

`~/.transifexrc`, which stores your Transifex host configuration in your home directory, including your API key.
`.tx/config`, which stores the mappings between your local files and Transifex in a .tx folder in your repo’s root directory.

Transifex’s own documentation for initialising the client involves running the tx init command. We are going to edit the files more directly.

##### Creating and storing your API key

You'll need a [Transifex API key](https://www.transifex.com/user/settings/api/) to push to and pull from the BODS project. Click on the “Generate a token” button on the right hand side. Click on “Copy and Close”. Your API token has been created.  You only need this locally; don't commit it or share it or store it anywhere public. 

So you don't have to enter it at the commandine every time you can store it in `.transifexrc` in your home directory (`~/`), which looks like:

```
[https://www.transifex.com]
api_hostname = https://api.transifex.com
hostname = https://www.transifex.com
password = YOUR-API-KEY-SHOULD-GO-HERE
username = api
```
Enter the lines as shown above, replacing YOUR-API-KEY-SHOULD-GO-HERE with your newly generated api key.

This sets you up with access to add and retrieve files to and from Transifex. See [Transifex client configuration](https://docs.transifex.com/client/client-configuration) for more details.

##### .tx/config

The `.tx/config` file is used to map files in a local repo/directory to resources in Transifex. This file is stored in the .tx folder in the repo’s root directory.

Although it is possible to pre-configure your `.tx/config` file in advance there are number of ways in which the configuration can change, right up until the moment that you extract and push your projects’ strings up to Transifex. In particular:

  * the project that you are pushing/pulling strings extracted from files to/from is specified in this file
  * our tooling automates the process of specifying the files that strings are extracted from (see [data-standard](https://github.com/openownership/data-standard)). This can be dependant upon the branch of the repo that you have checked out

For that reason, we often recreate the .tx/config file as part of the workflow.

The diagram below shows the state of the .tx/config file after extracting the strings from the 0.3 dev branch of the data-standard repo, ready to push those strings up to the BODS v0.3 project on Transifex.
  
![Github-Transifex config](https://github.com/openownership/bods-dev-handbook/blob/translation/screenshots/translation/github_transifex_config.png)

To create an initial `.tx/config` file follow the instructions in the [data-standard repo](https://github.com/openownership/data-standard)

## Integrating translations

Whenever any strings are changed that are in scope for translation (see list above) they need to be 'extracted', pushed to Transifex, translated, and the translated strings pulled back down. Updates to the documentation and schema should not be deployed until the necessary translations are in place.

The steps for doing this should be done by the person making the changes to the schema and docs, and are documented in the [data standard README](https://github.com/openownership/data-standard/blob/master/README.md). There are separate steps for the docs, schema and codelists, and you only need to carry out the steps applicable to the changes you made. For example, if you only updated the schema, you don't need to execute commands to extract strings from the docs or codelists.

The steps for the Sphinx theme are in the [sphinx theme README](https://github.com/openownership/data-standard-sphinx-theme#translations).

Note that 'extracted' (English) strings (`.pot` files) are not pushed to the github repo, but translated strings (`.po` files) are. This lets readthedocs find them so it can build everything in other languages. For a clean commit history, it's helpful to make separate commits for your changes to the source (docs or schema) and the translation files subsequently pulled from Transifex.

Note for developers: `.po` files from the Sphinx theme are included when you build the docs from `data-standard` thanks to the following line in `docs/conf.py`:

```
locale_dirs = ['locale/', os.path.join(oods.sphinxtheme.get_html_theme_path(), 'locale')]
```

So make sure the latest version of the theme is being installed in case expected translations aren't showing up.

## BODS on Transifex

BODS translations currently live under the Open Data Services Transifex account. The BODS docs and schema live in versioned projects, ie. v0.1 'project' is [bods-v01](https://www.transifex.com/OpenDataServices/bods-v01/dashboard/). The project contains 'resources', each of which correspond to a page of documentation (an individual RST file) plus one each for the schema, codelists and .svg files.

The documentation sphinx theme translations live under [bods-theme](https://www.transifex.com/OpenDataServices/bods-theme/dashboard/), which contains only one resource for all the strings in the theme templates.

### Teams and Roles

Teams are the groups of people who do the translations. Each project has just one team allocated to it, although a team can be allocated to more than one project. To illustrate this, below is a diagram showing the first ten projects listed under Open Data Services Co-operative (as at 2019-06-19) and the teams that are allocated to them. 

![Transifex: projects and teams](https://github.com/openownership/bods-dev-handbook/blob/translation/screenshots/translation/transifex_projects_and_teams.png)

A team can consist of the following roles:

  * A team manager
  * A team coordinator
  * Translators
  * Reviewers

The BODS team consists of a team manager, translators and reviewers, with the team manager taking on the role of coordinator. We also use subject matter experts to maintain the glossary. They do not have to use Transifex. Their work can be done in a spreadsheet that is uploaded to Transifex by the team manager. In the future we intend to host the glossary in the data-standard repository.

The BODS team manager allocates the translators and reviewers to a specific language. As at the time of writing we have only set up a team consisting of the [Members translating to Russian](https://www.transifex.com/OpenDataServices/teams/95583/ru/).

![Transifex: BODS Team](https://github.com/openownership/bods-dev-handbook/blob/translation/screenshots/translation/transifex_BODS_Team.png)

NOTE: The [OCDS handbook](https://ocds-standard-development-handbook.readthedocs.io/en/latest/standard/translation/workflow.html) specifies different roles. It separates out the "team manager" role into a "Release Manager" and a 'coordinator'. We should review these two different ways of working to see if we can agree a common standard. It also details a proofreader role which is not supported under our the Transifex free plan.

#### Team manager

Tasks:
  * Create the project
  * Co-ordinate the freeze on further development of the branch being translated
  * Push strings to be translated up to Transifex
  * Co-ordinate the work of the translators and reviewers
  * Pull translated and quality tested strings down from Transifex
  * Publish translated website using Read The Docs
  
Therefore they need:

Skills:
  * To have an understanding of how Github works
  * To understand and be able to manage the translation process in Transifex
  * To understand and be able to manage organisations and teams in Transifex
  * To be able to use the tooling to extract strings from the repositories
  * To be able to push and pull extracted strings to and from Transifex
  * To be able to add and update a translation of the website in Transifex

#### Translator

Tasks:
  * Translate the strings in Transifex from the source language (by default, English) into the target language

Therefore they need:

Skills:
  * To be native speakers of the target language and fluent in English (the source language)
  * To be confident in using, or learning to use, Transifex.

#### Reviewer

Tasks:
  * Review the translated strings in Transifex and provide feedback to translators and the team manager

Therefore they need:

Skills:
  * To be native speakers of the target language and fluent in English (the source language)
  * To have extensive experience of talking and writing about beneficial ownership in the target language
  * To be confident in using, or learning to use, Transifex
  * To have a pragmatic approach to translation, taking into account the wider context in which it may be used

#### Subject matter expert

Tasks:
  * Translate beneficial ownership terms from the glossary's source language into the target language, in an online spreadsheet (a Google sheet).
  * Make notes in that same spreadsheet about the selection or use of any particular terms. (For use by translators.)
  * Answer terminological queries from translators, if they come up.

Therefore they need:

Skills:
  * To be native speakers of the target language and fluent in English (the source language).
  * To have extensive experience of talking and writing about beneficial ownership in the target language.
  * To be confident in using, or learning to use, Google sheets.

### Access for translators

Translators should be given access to translate the main BODS project (documentation, schema, codelists), as well as the theme.

Translators and reviewers can follow the instructions here to sign up to Transifex: [Transifex docs for translators](https://docs.transifex.com/getting-started-1/translators).

Once a translator or reviewer has signed up to Transifex then an admiinistrator can add them to the BODS Team through the [BODS team > Members translating to Russian](https://www.transifex.com/OpenDataServices/teams/95583/ru/) page. Clicking on "Add translators" or "Add reviewers" will bring up this form

![Add collaborator](https://github.com/openownership/bods-dev-handbook/blob/translation/screenshots/translation/collaborate.png)

which can be completed to add the person to the project

#### The translation and review process

NOTE: This section describes a process that is different to how we have worked to date. As such it should be seen as a suggestion that is open to discussion.

##### Translators

Once the strings for the schema release have been uploaded to Transifex, the translator should be given access to the project and asked to begin the translation. 

Translators should be aware that they will be required to take part in the review of their work. Details of this are in the following section.

###### Reviewers

There are two inter-linked tasks for a reviewer. A reviewer can choose to do these separately or together as they work through the project.

1. Review all of the translated strings in the project
2. Check all of the warnings* against the translated strings in the project

*Transifex will warn users when certain translation checks fail. This includes cases when a term in the source file is translated to something other than the translation in the glossary.

Reviewers should make comments against the translation that are then resolved between them and the reviewer. 

Comments are made against a string. Because a string can consist of an entire paragraph it is necessary to quote the part of the string that a comment is made against. Because a reviewer might query more than one part of the string it is necessary to create a reference for the comment.

A comment template is as follows:

#1 "selection-of-text-being-commented-on"
- Description of the problem that the reviewer sees in the translation
- Suggestion how this can be resolved

The translator can then accept the suggestion by editing the translated string or they can reply to the reviewer with an alternative suggestion or a request for clarification. 

A template for a response to a comment is as follows

#1 "selection-of-text-being-commented-on"
- Response to the comment

##### Resolving differences
Where agreement cannot be reached by the translator and the reviewer it is the Team Manager's role to decide what should be done. They may take a decision themselves, or seek external advice.

### Changing schema version

BODS publishes documentation for each version of the schema, so when there's a version update we need a fresh Transifex project so earlier translations are not overwritten or removed.

* [Add a new project on Transifex](https://www.transifex.com/OpenDataServices/add/).
  * Name it according to the version of BODS, ie `bods-v02` for BODS version 0.2.
  * Choose 'public project' and **make sure to check the 'My project is a non-commercial Open Source project checkbox'** and enter the github repo URL.
  * ![Screenshot: tick the My project is a non-commercial Open Source project checkbox when creating a new project](screenshots/translation/transifex_noncommercial.png)
  * Assign the project to the BODS team.
* With your local branch for the new BODS version, after extracting the strings, run the commands for updating the Transifex config which are part of the usual flow whenever you add, remove or rename any files, but with the new Transifex project slug:

```
rm -f .tx/config
sphinx-intl create-txconfig
sphinx-intl update-txconfig-resources --pot-dir docs/_build/gettext --locale-dir docs/locale --transifex-project-name NEW-PROJECT-NAME-HERE
```

All the other steps for extracting strings and pulling down translations are as usual.

## Adding new languages on readthedocs

Once you've got all your translations, you need to actually publish them. The process for adding a new language version of the docs on readthedocs is a bit convoluted.

* Go to your [readthedocs dashboard](https://readthedocs.org/dashboard) and click 'Import a Project', then 'Import manually' to the right.
  * You probably want to name it something like "Beneficial Ownership Data Standard (LANG)"
  * The github URL is the base BODS repo, https://github.com/openownership/data-standard
  * Check the box for 'edit advanced project settings'
* Choose the language under Project Extra Details. The rest of the fields are intuitive, or have the right defaults.
* Go to Admin > Versions to activate any of the branches you need other than master. These should probably be the same ones as you have active in the main BODS readthedocs project, so the menus are consistent when the user switches language.
* Go to Builds to make sure the branch you need builds correctly. If it fails on a branch that the English version passes this is likely an indication that some translation files are missing. You can also preview it by clicking 'view docs'.
* Go back to the main (English) [BODS project](https://readthedocs.org/projects/beneficial-ownership-data-standard/). In Admin > Translations, choose the new project you just created from the Project dropdown:
  * ![Screenshot: add a readthedocs subproject](screenshots/translation/rtd_addtranslation.png)
* The new language should now appear as an option in the readthedocs flyout menu for all versions of the HTML documentation.

These instructions were summarised from [Localization of Documentation](https://docs.readthedocs.io/en/stable/localization.html) in the readthedocs docs.

## Previewing on readthedocs

When work is in progress on a branch, you can build this branch in readthedocs to preview it before publishing.

* Push local changes and translations to your in-progress branch github.
* Go to the readthedocs project for the particular language version of the docs you want to preview.
* If you have never built this branch before, you need to nudge readthedocs into seeing it; build any other branch, eg. latest:
  * ![Screenshot: building an existing branch](screenshots/translation/rtd_preview_build1.png)
* Go to Versions on the main menu. Find your branch on the list of inactive branchs and click Edit on the right. 
  * ![Screenshot: activating a new branch](screenshots/translation/rtd_preview_build2.png)
* Check 'Active' and set the dropdown to 'Protected' (this means the URL will work for sharing, but it won't appear in the versions menu):
  * ![Screenshot: activating a new branch](screenshots/translation/rtd_preview_build3.png)
* Go to Builds. Your new branch should have already built automatically and appear at the top of the list, but if it hasn't you can choose it from the dropdown and click 'Build'. You can see the results by clicking on the latest build:
  * ![Screenshot: the results of a readthedocs build](screenshots/translation/rtd_preview_built.png)
* You can preview it by clicking the green 'view docs' button in the top right.
* You can rebuild it from the dropdown at the top of the Builds page every time you push new changes to github.
* Don't forget to switch it off when you're done in Admin > Versions.

## Additional resources

* [Using Transifex (OCDS docs)](https://ocds-standard-development-handbook.readthedocs.io/en/latest/standard/translation/using_transifex/)
* [OCDS translation workflow](https://ocds-standard-development-handbook.readthedocs.io/en/latest/standard/translation/workflow/)
* [OCDS technical implementation of translation](https://ocds-standard-development-handbook.readthedocs.io/en/latest/standard/translation/implementation/)
* [Readthedocs translation workflow](https://docs.readthedocs.io/en/stable/guides/manage-translations.html)
