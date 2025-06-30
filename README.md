# Beneficial Ownership Data Standard - Development handbook

This repo contains work-in-progress documentation for people who are working *on* the Beneficial Ownership Data Standard. It is published on [github pages](https://openownership.github.io/bods-dev-handbook/) to keep it lightweight and easy to update. The source files are at [github.com/openownership/bods-dev-handbook](https://github.com/openownership/bods-dev-handbook).

To this repo you can add meta-documentation around updating the standard itself - workflows, processes, technical things and administrivia that you don't want to be siloed inside your own organisation's CRM or private wiki, but that don't need to be seen by people who are only publishing or consuming data which conforms to the standard. Do check to make sure what you want to add wouldn't be better suited to the docs of a particular tool.

If you add a new page, please follow the editing advice below, and list it under 'Contents' here.

## Contents

* [The BODS feature development pipeline](feature_development.md)
* BODS schema development
  * [Git Branches, Version Numbers and Standard Releases](standard_releases.md)
  * [Maintenance and compilation of the BODS schema](compiling_schema.md)
  * [Testing and metaschema extensions](testing.md)
  * [Updating the JSON schema version](json_schema_version_updates.md)
* BODS documentation writing
  * [Creating SVG diagrams](diagram_creation.md)
  * [Style Guide](style_guide.md)
* [BODS translations](translations.md)
* [Tools for working with BODS](tools.md)
* [Data Validation Tool (BODS CoVE)](data_validation.md)


## Not contents

It does **not** contain:

* A guide to using the BODS schema - see [BODS documentation](https://standard.openownership.org)
* Information about BODS governance - see [BODS documentation](https://standard.openownership.org/en/latest/about/index.html)
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

## Editing this handbook

This Handbook is in English only (no translations).

Currently, there is no requirement for pull requests to be made - you can edit content on the main branch directly. Later, that will change to a strict requirement to always use pull requests.

### Previewing work you have done

If you want to preview work before pushing it live, create a new branch in Git. Go to the GitHub UI, select the file you want to see and a preview is shown.

But be aware; there are some differences between this preview and the real docs on GitHub pages. These are:

### Links

If you just put a link in some text like this:

    Please go to http://example.com/

It will appear as a clickable link in the preview but NOT in github pages. To make the link clickable in Github pages, use angle bracket markdown:
    
    Please go to <http://example.com/>

Or use the bracket notation:

    Please go to [http://example.com/](http://example.com/)

Or more readable-

    Please go to [example.com](http://example.com/)

