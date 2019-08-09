# Maintenance and compilation of the BODS schema

## Codelists
_[We maintain codelists as csv files so that we can included metadata for codelist items. We should document here what the workflow is around updating them and embedding codelist items as enums in the schema. OCDSkit has 'set-closed-codelist-enums' (Sets the enum in a JSON Schema to match the codes in the CSV files of closed codelists). Does BODSkit have sthg similar, should it? And should compilation (below) call on that operation?]_


## Compilation

The definitive version of the schema is files in https://github.com/openownership/data-standard/tree/master/schema , starting with "bods-package.json". "bods-package.json" references other files in that folder.

You may want to compile a version:

  *  You may be using a tool that has problems with refs, so you need a complete version of the schema in one file.
  *  There are some non-standard JSON Schema options we use and as they are compiled into one file using our tool, you get one file that is standard JSON Schema.

To compile a version, use our tool: https://github.com/OpenDataServices/compile-to-json-schema

    compiletojsonschema openownership-data-standard/schema/bods-package.json  > compiled_schema.json




