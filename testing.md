# Testing the schema

## Metaschema

BODS v0.4 uses JSON Schema 2020-12 as its base metaschema, extended with some custom properties which are used to further constrain the BODS schema. These are:

* `codelist` (string): The filename of a .csv in the BO Data Standard which defines the allowed values for this property.
* `openCodelist` (boolean): If true, the property can contain values beyond what is defined in the codelist in the BO Data Standard. If false,the property is restricted to only the values defined in the codelist.
* `version` (string): The BODS schema version number.
* `propertyOrder` (integer): The order in which properties should be displayed for optimised user experience. Properties whose values are not objects or arrays should be listed first.
* `oneOfEnumSelectorField` (string): Hints to a validator which subschema to use when validating objects which may use one of several schema options, in order to improve error messages.

Properties from the extended metaschema should not be present in any BODS _data_, only in the _schema_. Therefore they don't need to be documented for data publishers, only for schema architects and developers.

The metaschema file is found in `data-standard/tests/schema/meta-schema.json`. As part of the data standard repository tests, the BODS schema files are validated against the metaschema.

## Python tests

Test files are found in the `data-standard/tests` directory.

Tests for the BODS schema are organised into:

* CSV tests: These validate the codelist CSV files.
* Schema tests: These validate the structure of the schema files, and compliance with the [metaschema](#metaschema).
* Data tests: These test the schema against valid and invalid sample data, to check that the schema constrains data as expected. Data for these tests is organised in several subdirectories under `data-standards/tests/data`.
* Docs tests: These test the data snippets and example data used in the data standard documentation, to make sure they are formatted correctly and valid BODS data.

The tests are written using pytest. Fixtures for loading the schema, creating a validator, and other helper functions can be found in `conftest.py`.

The tests and a flake8 code quality check are run automatically when a branch is pushed to the `data-standard` repository.

### Code quality

We use  [Black](https://pypi.org/project/black/), * [iSort](https://pypi.org/project/isort/) and [flake8](https://pypi.org/project/flake8/) for code linting. Pull requests are automatically checked and must pass these before they can be merged.

### Running tests locally

Tests can be run in your local development environment (ie. in a virtualenv or docker container or similar) from inside the `data-standard` repository.

Make sure the test requirements are installed, ie.:

```bash
pip install -r requirements_test.txt
```

To run all the tests:

```python
pytest tests/
```

To run one set of tests:

```python
pytest tests/test_csv.py
```

### Adding tests
