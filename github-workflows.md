# GitHub workflows 
The GitHub repository includes some automated tests which run when a branch is pushed to or a pull request is made. 

## Spellchecker 

Spellchecker is an automatic spellchecker which reviews the BODS documentation for spelling errors. 

### wordlist 

If a word is not in the [Aspell en_gb-ise dictionary](http://app.aspell.net/lookup) but is a valid word you need to add it to the .github/workflows/.wordlist.txt file in the BODS repository. This file has one word per row and is case sensitive. 

### configuration 

In the configuration file .spellcheck.yml (in the main repo not in the github/workflows folder) there are a number of configuration options. 

#### sources

sources is used to direct which files should be checked for spelling errors. Currently this is only set up to check the docs folder

#### filters 

pyspelling filters direct the spellchecker to ignore certain content. 

`pyspelling.filters.url` and `pyspelling.filters.html` set it to ignore URLs and HTML snippets. 

`pyspelling.filters.context` sets custom [context filters](https://facelessuser.github.io/pyspelling/filters/context/) 

`context_visible_first: true` indicates that content will be checked for spelling errors until the context filter is in effect

`delimiters` define when the context filters should take effect. `open` and `close` set the boundaries of the filters. See [this issue](https://github.com/facelessuser/pyspelling/discussions/204#discussioncomment-13531926) where we received advice on using context filters to filter out RST content.

#### Aspell

The spellchecker uses the [Aspell en_gb-ise dictionary](http://app.aspell.net/lookup)

## Link check 

Linkcheck checks for broken links in the documentation. 

When a link is broken the test fails and the link is listed as "broken" in the log. The log presents the full list of links so search the logs for the word "broken" to find the broken link. 

## Docs build

Checks the docs are building
