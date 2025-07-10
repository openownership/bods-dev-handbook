# Test-driven Schema Development

Before making any changes to the schema, ensure you understand the test framework in the repository, described below. Changes to the schema should not be merged until all of the changes are covered by tests, and the tests pass.

Exceptions may be made for rapid iteration on pre-release changes, where test coverage/failure is documented, and expected to be resolved before a new version is released.

In summary, we test:

* Example data (in the docs) is valid and well-formed.
* The schema and codelists are well-formed and valid JSON.
* The constraints expressed in the JSON schema work as expected to validate data.

This last category of tests facilitate [test-driven development](https://agilealliance.org/glossary/tdd/) of the schema. The approach to changing or adding fields within the schema, introducing or changing constraints, should be to:

1. [Run the python tests](testing.md#running-tests-locally) to see that they are all passing
2. [Add](testing.md#schema-function) sets of BODS JSON data which should be valid or invalid according to the new constraints (fixtures)
3. Run the python tests again, noticing that they likely fail because the schema has not been updated
4. Update the schema, introducing or changing its constraints, and then run the python tests.
5. Repeat (4) until all tests are passing as expected.
6. Update the [validation specification](data_validation.md).


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

After adding new files make sure to **run the tests** (`pytest tests/test_data.py`) to check they pass.

##### Testing against valid data

A minimum valid BODS entity statement looks like this:

```
[
    {
        "statementId": "2f7bf9370f1254068e5e946df067d07d",
        "declarationSubject": "xyz",
        "statementDate": "2017-11-18",
        "recordId": "123",
        "recordType": "entity",
        "recordDetails": {
            "entityType": {
                "type": "unknownEntity"
            },
            "isComponent": false
        }
    }
]
```

Start from a minimal statement like this, and add only the field you are testing. If you are testing a field in a nested object (eg. `publicationDetails/publisher/name`) you may need to add more data to cover additional required fields (eg. `publicationDetails/publicationDate`). Check the schema itself to find out which fields are required for the various objects.

##### Testing against invalid data

As with valid data, start from a minimal valid statement and add invalid values (or remove in the case of a required field) for only the field you are testing. There should be **one validation error per file** only. The test will fail if there is more than one.

We also have to **test that the validation error is the one we expect**, so we need to map the data files to the type and location of the error we're looking for. Do this by updating `expected_errors.csv` (in the same directory as the invalid data). The structure of this file is:

* file name (eg. "entity_addressType_placeOfBirth.json")
* validation keyword (the type of error we expect, eg. "enum")
* json path (the path to the location of the error in the data being tested, eg. "$[0].recordDetails.addresses[0].type")
* property (the property in the data which is the subject of the test)

**Validation keywords** are from [the JSON Schema standard](https://json-schema.org/draft/2020-12/meta/validation), and are one of:

* `required`: the property is missing
* `type`: the value is the wrong data type
* `const`: the value is not the one required by the schema
* `enum`: the value is not one of a set required by the schema
* `multipleOf`: the value is not the multiple required
* `maximum`: the value is too high
* `exclusiveMaximum`: the value is too high
* `minimum`: the value is too low
* `exclusiveMinimum`: the value is too low
* `maxLength`: the value is too long
* `minLength`: the value is too short
* `pattern`: the value does not match the defined pattern
* `maxItems`: the array has too many items
* `minItems`: the array has too few items
* `uniqueItems`: the array contains duplicates
* `maxContains`: the array contains to many items of the type allowed by the `contains` subschema
* `minContains`: the array contains too few items of the type allowed by the `contains` subschema
* `maxProperties`: the object contains too many properties
* `minProperties`: the object contains too few properties
* `dependentRequired`: a property dependent on another property is missing

The validation keyword may sometimes need to be set to `oneOf`, `anyOf` or `allOf` if a value is constrained by multiple possible subschemas, rather than the keyword actual validation that is taking place. Making this more precise is a todo.

**The JSON path** always begins with `$[0]` because each test file is an array of one statement. The path is separated by `.`. Elements in arrays are represented by `[0]`, `[1]`, etc. for the position of the error in the array. When the error relates to a missing required field, the JSON path ends at the parent. ie. To test a missing `statementDate`, the JSON path is `$[0]` (because that is the location of the required field error), _not_ `$[0].statementDate`.

**The property** is the name of the specific field you're testing. To test a missing `statementDate`, set this value to `statementDate`. To test an incorrect address type, set this to `type`.

#### Docs and examples

* If example data is added or removed from the `/examples` directory, you don't need to make any changes to the tests - these are picked up and validated automatically.
