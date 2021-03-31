# Maintenance and compilation of the BODS schema

## Codelists

Codelists are maintained as csv files so that metadata for codelist items can be included. Values of closed codelists are duplicated in JSON schema files for any schema that use them as `enum`s. Eg. the Entity Type codelist is defined in the `entityType.csv` file, and appears in the `entity-statement.json` schema like so:

```
"entityType": {
    ...
    "enum": [
        "registeredEntity",
        "legalEntity",
        "arrangement",
        "anonymousEntity",
        "unknownEntity"
      ],
      "codelist": "entityType.csv",
      "openCodelist": false,
      ...
}
```

To update an existing codelist:

* Edit the CSV file
* Find all schema which use it, and edit the `enum` values to match.
* Run the tests (run `pytest` in the `data-standard` repo) to make sure you haven't missed anything or made any typos.

To add a new codelist:

* Create a new CSV file in the `schema/codelists` directory with the column headings:
  * code
  * title
  * description
  * technical note
* If it is a closed codelist, add or update the `enum`, `codelist` and `openCodelist` properties for any properties in the JSON schema(s) which should reference it.
* Run the tests to make sure you didn't miss anything.

To remove a codelist:

* Delete the CSV file
* Remove all references to the CSV file from the schema JSON files.
* Run the tests to make sure you haven't missed any.

The tests will catch any codelists that aren't used in any schema, as well as any schema which reference codelist CSVs that do not exist. The tests also check the `enum` values against the `code` column in the equivalent codelist CSV to make sure the values match exactly. The only exception to this is the `statementType` codelist, as each type of statement is constrained to only one value from the codelist, so it is skipped by the tests.

## Compilation

The definitive version of the schema is files in https://github.com/openownership/data-standard/tree/master/schema , starting with "bods-package.json". "bods-package.json" references other files in that folder.

You may want to compile a version:

  *  You may be using a tool that has problems with refs, so you need a complete version of the schema in one file.
  *  There are some non-standard JSON Schema options we use and as they are compiled into one file using our tool, you get one file that is standard JSON Schema.

To compile a version, use our tool: https://github.com/OpenDataServices/compile-to-json-schema

    compiletojsonschema openownership-data-standard/schema/bods-package.json  > compiled_schema.json




