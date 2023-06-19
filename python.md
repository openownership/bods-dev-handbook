# Python development

This page describes how to develop Python in BODS. 
There are some bits of Python in the standards repository, and some Python software repositories.

To a large extent, different repositories may have their own practices.

Every repository should have documentation within the repository. Look in the `README` file or the `docs` directory.

## Code linting - Black, isort & flake8

Generally speaking we try to use the following tools for code linting:

* [Black](https://pypi.org/project/black/)
* [iSort](https://pypi.org/project/isort/)
* [flake8](https://pypi.org/project/flake8/)

Normally a GitHub Action set up to enforce these in pull requests.

Open Data Services has [more documentation on how they tend to use these](https://opendataservices.gitbook.io/developer-docs/reference/python/code-standards).

## Tests

Tests should be written in [Pytest](https://pypi.org/project/pytest/), or the Django test framework.

Normally a GitHub Action set up to enforce these in pull requests.

