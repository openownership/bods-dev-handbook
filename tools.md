# Tools for working with BODS

## BODS Documentation

BODS docs are published on [readthedocs](https://standard.openownership.org).

## Building the docs using the development environment 
### Installing the development environment 
Install the ODSC development environment by following the instructions at https://github.com/OpenDataServices/development-environment

The setup process guides you through several options
- For 'Please select a container management engine to use' either will work (use Docker if you don't have a preference) 
- For 'Do you want to mirror the environment's working directory locally?' select 'yes'
- Select your preferred text editor to be installed (use Pycharm if you don't have a preference)
- Select 'Beneficial Ownership Data Standard (BODS)' to be installed in the environment
- Do you want to setup a new development branch? Select 'no' unless you want to set one up

### Building the docs
Open a terminal and navigate to the development environment 

``cd development-environment``

connect to the environment 

``bin/connect``

navigate to the data standard 

``cd development/data-standard/``

run sphinx build

``sphinx-build docs/ _build``

navigate to _build 

``cd _build``

open the docs in a server 

``python3 -m http.server``

then open http://0.0.0.0:8000/ in a browser window to view the docs 

## BODS docs theme and vagrant box

The latest version of the BODS docs automatically uses the lastest version of the theme from the repo. Older versions of the docs may be pinned to specific commits or branches of the theme.

If you need to work on the docs and test how they build, you can use a Python virtual environment, as outlined in the [data standard ReadMe](https://github.com/openownership/data-standard#build--test-the-docs-locally).

If you need to work on the docs theme and test changes to it, you can use the vagrant virtual box provided in the theme repository.

[ [Data standard ReadMe](https://github.com/openownership/data-standard#build--test-the-docs-locally)  |  [Theme repository](https://github.com/openownership/data-standard-sphinx-theme) ]

## OCDSKit

OCDSkit provides command line tools for common development tasks, which can also be used with BODS.

[ [OCDSkit documentation](https://ocdskit.readthedocs.io/en/master/cli.html) | [Repository](https://github.com/openownership/ocdskit) ]

## Flatten Tool for BODS

Flatten-Tool enables a dataset to be round-tripped between structured JSON and tabular data packages, CSV files, or spreadsheets.

[ [Flatten Tool documentation](https://flatten-tool.readthedocs.io/en/latest/usage-bods/) | [Repository](https://github.com/OpenDataServices/flatten-tool) ]

## Tools for producing an updated field mapper

[BODSkit](https://github.com/openownership/bodskit) used to contain various
software tools which could be used when working on the field mapping spreadsheet.

That repository has since been archived, because all of the tools could be
found elsewhere, either in other open-source packages or in OCDSkit.

Here are the replacements for the existing tooling:

### Extracting a spreadsheet with all of the fields from the schema

Before:

`bodskit mapping-sheet ~/work/openownership-data-standard/schema/person-statement.json > out.csv`

Now:

`ocdskit mapping-sheet --order-by path ~/work/openownership-data-standard/schema/person-statement.json > out.csv`

### Combining all codelist CSVs into a single file

Before:

`bodskit all-codes ~/work/openownership-data-standard/schema/codelists > out.csv`

Now:

```shell
pip install csvkit
cd path/to/data-standard
csvstack --filenames -n codelist schema/codelists/* | sed s/\.csv// | in2csv -f csv
```

### Report open and closed codelists in a schema

Before:

`bodskit schema-codelist-report ~/work/openownership-data-standard/schema/person-statement.json`

Now:

`ocdskit schema-report --no-definitions ~/work/openownership-data-standard/schema/person-statement.json`

(Note the `type` column now becomes a boolean `openCodeList` column, but the
meaning is identical)

## Locally running CoVE checks on the command line for schema development
_This is a hacky way of doing things. Please edit with any improved process_

**Goal:** run command line validation and additional checks of example data against dev version of schema.

* have some kind of virtual environment for doing BODS things in;
* git clone and install [lib-cove-bods](https://github.com/openownership/lib-cove-bods) using `pip install -e .`;
* make a branch of lib-cove-bods to do your dev work in;
* git clone and install [Compile to JSON Schema Tool](https://github.com/OpenDataServices/compile-to-json-schema) per the docs.
* change the BODS schema;
* use JSON Schema Tool to compile the new bods-package schema into the lib-cove-bods [data](https://github.com/openownership/lib-cove-bods/tree/master/data) folder: `compiletojsonschema path/to/bods-package.json > path/to/lib-cove-bods/data/schema-X-Y-Z.json` X-Y-Z should be version number of the schema. You can temporarily alter the schema for an existing version, or make a new version of the schema.
* if you have chosen to create a new version of the schema, you will also need to update the libcovebods/config.py file in lib-cove-bods by adding in the new schema. 
* The `schema_versions` setting maps the value of the bodsVersion field in the data to the schema file the tool will check it against.
* The easiest way to add in the new schema is to copy the block of code for an existing schema and paste into the array (make sure of the right bracket level);
* The text before the colon is the name of the schema used by the code - update this to reflect the bodsVersion that will be referenced in the json files;
* Within schema_url update the filename to reflect the new json schema file that was added to the lib-cove-bods/data directory earlier;
* Update `schema_latest_version` to point to the schema name defined earlier.
* use lib-cove-bods to validate some example data against the new compiled schema: `libcovebods path/to/example.json`
