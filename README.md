# Beneficial Ownership Data Standard - Development handbook

This repo contains work-in-progress documentation for people who are working *on* the Beneficial Ownership Data Standard. It is published on [github pages](https://openownership.github.io/bods-dev-handbook/) to keep it lightweight and easy to update.

To this repo you can add meta-documentation around updating the standard itself - workflows, processes, technical things and administrivia that you don't want to be siloed inside your own organisation's CRM or private wiki, but that don't need to be seen by people who are only publishing or consuming data which conforms to the standard. Do check to make sure what you want to add wouldn't be better suited to the docs of a particular tool.

If you add a new page, please list it on the contents below.

## Contents

* Principles for working with BODS
  * [Style Guide](style_guide.md)
* [Tools for working with BODS](tools.md)
* [CoVE Translations](cove_translations.md)
* [Translations](translations.md)
* [Maintenance and compilation of the BODS schema](compiling_schema.md)
* [Git Branches, Version Numbers and Standard Releases](standard_releases.md)
* [This handbook](this_handbook.md)

## Not contents

It does **not** contain:

* A guide to using the BODS schema - see [BODS documentation](https://standard.openownership.org)
* Information about BODS governance - see [BODS documentation](http://standard.openownership.org/en/latest/about/index.html)
* How to build the BODS docs - see [BODS Sphinx Theme](https://github.com/openownership/data-standard-sphinx-theme)
* Deployment information - see [?](#) (internal to Open Data Services Co-op).
* Any keys, passwords, or configuration files.

## Running this site locally

The site uses jekyll (through github-pages) to turn these markdown files into
html. You can do so locally too, to preview changes:

* Install Ruby and Bundler. Github pages' [prerequisites section](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll#prerequisites)
  provides documentation on how to do that for Mac, Windows and Linux.
* `cd` into your local checkout of this repo
* Install the Ruby gems from this repository with Bundler: `bundle install`
* Run `bundle exec jekyll serve`
* Visit `https://localhost:4000`
