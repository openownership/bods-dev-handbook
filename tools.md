# Tools for working with BODS

## BODS Documentation

BODS docs are published on [readthedocs](http://standard.openownership.org).

## OCDSKit
OCDSkit provides command line tools for common development tasks, which can also be used with BODS.

[ [OCDSkit documentation](https://ocdskit.readthedocs.io/en/master/cli.html) | [Repository](https://github.com/openownership/ocdskit) ]

## Flatten Tool for BODS
Flatten-Tool enables a dataset to be round-tripped between structured JSON and tabular data packages, CSV files, or spreadsheets.

[ [Flatten Tool documentation](https://flatten-tool.readthedocs.io/en/latest/usage-bods/) | [Repository](https://github.com/OpenDataServices/flatten-tool) ]

## Locally running CoVE checks on the command line for schema development
_This is a hacky way of doing things. Please edit with any improved process_

**Goal:** run command line validation and additional checks of example data against dev version of schema.  

* have some kind of virtual environment for doing BODS things in;
* git clone and install [lib-cove-bods](https://github.com/openownership/lib-cove-bods) using `pip -r requirements.txt`;
* make a branch of lib-cove-bods to do your dev work in;
* git clone and install [Compile to JSON Schema Tool](https://github.com/OpenDataServices/compile-to-json-schema) per the docs.
* change the BODS schema;
* use JSON Schema Tool to compile the new bods-package schema into the lib-cove-bods [data](https://github.com/openownership/lib-cove-bods/tree/master/data) folder: `compiletojsonschema path/to/bods-package.json > path/to/lib-cove-bods/data/schema-X-Y-Z.json` X-Y-Z should be version number of the schema. You can temporarily alter the schema for an existing version, or make a new version of the schema.
* if you have chosen to create a new version of the schema, you will also need to update the libcovebods/config.py file in lib-cove-bods. The `schema_versions` setting maps the value of the bodsVersion field in the data to the schema file the tool will check it against.
* use lib-cove-bods to validate some example data against the new compiled schema: `libcovebods path/to/example.json`
