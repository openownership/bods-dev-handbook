# Testing the schema

Changes to the schema should not be merged until all of the changes are covered by tests, and the tests pass.

Exceptions may be made for rapid iteration on pre-release changes, where test coverage/failure is documented, and expected to be resolved before a new version is released.

In summary, we test:

* Example data (in the docs) is valid and well-formed.
* The schema and codelists are well-formed and valid JSON.
* The constraints expressed in the JSON schema work as expected to validate data.

## Metaschema

BODS v0.4 uses JSON Schema 2020-12 as its base metaschema, extended with some custom properties which are used to further constrain the BODS schema. These are:

* `codelist` (string): The filename of a .csv in the BO Data Standard which defines the allowed values for this property.
* `openCodelist` (boolean): If true, the property can contain values beyond what is defined in the codelist in the BO Data Standard. If false,the property is restricted to only the values defined in the codelist.
* `version` (string): The BODS schema version number.
* `propertyOrder` (integer): The order in which properties should be displayed for optimised user experience. Properties whose values are not objects or arrays should be listed first.

Properties from the extended metaschema should not be present in any BODS _data_, only in the _schema_. Therefore they don't need to be documented for data publishers, only for schema architects and developers.

The metaschema file is found in `data-standard/tests/schema/meta-schema.json`. As part of the data standard repository tests, the BODS schema files are validated against the metaschema.

## Python tests

Test files are found in the `data-standard/tests` directory.

Tests for the BODS schema are organised into:

* Schema tests: These validate the structure of the schema files (including codelist CSVs), and compliance with the [metaschema](#metaschema).
* Data tests: These test the schema against valid and invalid sample data, to check that the schema constrains data as expected. Data for these tests is organised in several subdirectories under `data-standards/tests/data`.
* Docs tests: These test the data snippets and example data used in the data standard documentation, to make sure they are formatted correctly and valid BODS data.

The tests are written using pytest. Fixtures for fetching files, loading the schema, creating a validator, and other helper functions can be found in `conftest.py`.

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

To run one set of tests, eg.:

```python
pytest tests/test_schema.py
```

To run code linting:

```python
flake8 tests/
```

(There is no output if all the code is conformant.)

and:

```python
black tests/ --line-length=119
```

### Adding tests

The tests in the [data standard repository](https://github.com/openownership/data-standard) are present to validate that the _JSON Schema_ works as expected. They are not to validate _data_, and don't test any requirements imposed on data by the data standard which are not enforced by the JSON Schema - these should be covered by a validation tool.

#### Schema structure

* If a schema file is added or removed, or an `$id` value is changed, the `schemas` variable needs to be updated in `test_schema.py`.
* If additional requirements are placed on how the schema is structured or formatted (eg. letter case of fields, indentation) tests for these should be added to `test_schema.py`.
* New codelists are tested automatically; nothing needs to be added if these change.

#### Schema function

If constraints are added to or removed from the JSON schema (eg. a string field which previously had no maximum length now has a maximum length), valid and invalid test data should be added to the appropriate subdirectory in `tests/data/`.

Use one file per requirement, with the minimum contents possible to test only the requirement in question. This is so that if any requirements change in future, we have the minimum amount to update in the test files.

Name the test files to make it clear which requirement is being tested.

A minimum valid BODS entity statement looks like this:

```
[
    {
        "statementId": "2f7bf9370f1254068e5e946df067d07d",
        "declarationSubject": "xyz",
        "recordId": "123",
        "recordType": "entity",
        "recordDetails": {
            "entityType": "unknownEntity",
            "isComponent": false,
        },
    }
]
```

Start from a minimal statement like this, and add only the field you are testing. If you are testing a field in a nested object (eg. `publicationDetails/publisher/name`) you may need to add more data to cover additional required fields (eg. `publicationDetails/publicationDate`). Check the schema itself to find out which fields are required for the various objects.

After adding new files make sure to **run the tests** (`pytest tests/test_data.py`) to check they pass.

#### Docs and examples

* If example data is added or removed from the `/examples` directory, you don't need to make any changes to the tests - these are picked up and validated automatically.
