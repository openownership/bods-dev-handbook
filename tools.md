# Tools for working with BODS

## Documentation

BODS docs are published on [readthedocs](http://standard.openownership.org).

## BODSkit
BODSkit provides command line tools for common development tasks.

[ [BODSkit documentation](https://bodskit.readthedocs.io/en/master/cli.html) | [Repository](https://github.com/openownership/bodskit) ]


## Locally building CoVE for schema development
_This is a hacky way of doing things. Please edit with any improved process_

**Goal:** run command line validation and additional checks of example data against dev version of schema.  

* have some kind of virtual environment for doing BODS things in;
* git clone and install [lib-cove-bods]() using `pip -r requirements.txt`;
* make a branch of lib-cove-bods to do your dev work in;
* git clone and install [Compile to JSON Schema Tool](https://github.com/OpenDataServices/compile-to-json-schema) per the docs.
* change the BODS schema;
* use JSON Schema Tool to compile the new bods-package schema into the lib-cove-bods [data](https://github.com/openownership/lib-cove-bods/tree/master/data) folder: `compiletojsonschema path/to/bods-package.json > path/to/lib-cove-bods/data/schema.json`
* use lib-cove-bods to validate some example data against the new compiled schema: `libcovebods path/to/example.json`
