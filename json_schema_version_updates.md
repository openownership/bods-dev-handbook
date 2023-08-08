# JSON Schema version updates

## Upgrading the BODS schema

Work through all of the JSON schema terms we use in the BODS schema, and find out if any of them:

1. have been deprecated or replaced.
2. have changed in meaning or usage.

Then review any major changes between the two JSON schema versions, and assess if there are any new terms or features we can make use of to improve our ability to validate data against the BODS schema.

## Validation and testing

The tests import a specific validator version from the Python jsonschema library. This will need to be updated when the version of JSON Schema used changes.

We extend JSON Schema with a few custom properties which are applied in the metaschema. The file `meta-schema.json` (found in `data-standard/tests/schema`) contains a copy of the current JSON Schema version, plus the custom properties. This will need to be updated when changing the JSON Schema version.

For a description of custom properties currently in use, see [Metaschema](testing#metaschema).

It's likely that the testing dependencies of [jsonschema](https://python-jsonschema.readthedocs.io/en/stable/) and [JSCC](https://jscc.readthedocs.io/en/latest/) will need to be updated to accommodate JSON Schema version upgrades.

## Migrating the data

Updating the BODS schema to use a later version of JSON Schema may mean that BODS data which conforms to the old version of the BODS schema is no longer conformant; in this case, the BODS schema update is non-backwards-compatible. It is advisable to couple any non-backwards-compatible JSON Schema updates with a version update to BODS as a whole, so that published data does not need to be migrated to remain valid.

Data used for examples and testing will need to be migrated to the new version.

Changes which affect a small number of data items may be simple to make by hand. Changes which affect large numbers of data items, or which are complex, may need to be scripted. When updating the JSON Schema version, keep track of how the changes may affect existing data, and provide guidence or scripts for data migration if necessary.

# Update from draft-04 to 2020-12

The JSON Schema version update was applied to version 0.3 of the BODS schema.

## Changes

| From | To | Notes |
| ==== | == | ===== |
| `id` | `$id` | Must resolve to an absolute URI. Should not contain a fragment. |
| `definitions` | `$defs` | |
| `exclusiveMinimum`, `exclusiveMaximum` | changed from bool to number | "wherever one of these would be true before, change the value to the corresponding "minimum" or "maximum" value and remove the "minimum"/"maximum" keyword" |
| `items` | `prefixItems` | not applicable to BODS 0.3 |
| `additionalItems` | `items` | not applicable to BODS 0.3 |
| `enum` | `const` | where `enum` contains one element |


## Additions

New terms/functionality that may be useful:

* contains, maxContains, minContains
* const
* duration
* uuid
* date
* time
* regex
* if/then/else
* examples
* $comment
* $vocabulary for metaschema

_(This section will be updated as new terms are integrated into the BODS schema)_

## Documentation

* Update schema documentation about `minimum`/`exclusiveMinimum`/`maximum`/`exclusiveMaximum`
  * While you can specify both of `minimum `and `exclusiveMinimum` or both of `maximum` and `exclusiveMaximum`, it doesn’t really make sense to do so.
  * `Interest / share / maximum` has gone from exclusive by default to inclusive. `exclusiveMaximum` now needs to be used instead

## Data

* change `maximum` to `exclusiveMaximum`, unless:
  * it's representing exact values
  * `exclusiveMaximum` is present and set to `false`
* if `exclusiveMaximum` is present and set to `false`:
  * remove the boolean `exclusiveMaximum`
* if `exclusiveMinimum` was set to `true`:
  * change `minimum` to `exclusiveMinimum` and remove the boolean `exclusiveMinimum`

In the BODS schema, this is applicable to `Interest / share / maximum` and `Interest / share / minimum`.

## Working notes

`id` -> `$id`
`version`
`type`
`items`
`oneOf`
`$ref`
anyOf
title
description
required
additionalProperties
properties
exclusiveMinimum
exclusiveMaximum
minItems
uniqueItems
definitions -> `$defs`
enum
format
minLength
maxLength
pattern
items
default



types:

object
string
array
null

formats:

date-time
date
uri


### draft-06

* id -> $id. Must resolve to an absolute URI
* $ref only allowed where a schema is expected
* exclusiveMinimum/Maximum - changed from boolean to number. "wherever one of these would be true before, change the value to the corresponding "minimum" or "maximum" value and remove the "minimum"/"maximum" keyword"
* propertyNames - validates names of properties rather than values
* contains - array keyword that passes validation if its schema validates at least one array item
* const - one element enum
* required: {} means no properties are required
* examples

New formats:

* uri-reference (for relative rather than absolute)
* uri-template
* json-pointer

### draft-07

* No keywords changed behaviour or removed
* New keywords of interest:
  * $comment
  * if/then/else 
* New formats of interest:
  * date
  * time
  * regex


### 2019-09

* $id should not contain a fragment (empty discouraged)
* $anchor - replaces plain name form of id
* definitions -> $defs
* dependencies -> dependentSchemas and dependentRequired (string form)
* other keywords are now allowed alongside $ref
* $vocabulary - supported keywords in metaschema
* unevaluatedItems - additionalItems but in subschemas and refs
* unevaluatedProperties - as above
* maxContains, minContains
* format validation off by default
* deprecated

New formats:

* duration
* uuid (RFC4122)

### 2020-12

* items -> prefixItems
* additionalItems -> items
* $dynamicRef/Anchor

Stuff on bundling and compound schema documents