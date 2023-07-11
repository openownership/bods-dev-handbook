# JSON Schema version updates

## Upgrading the BODS schema

Work through all of the JSON schema terms we use in the BODS schema, and find out if any of them:

1. have been deprecated or replaced.
2. have changed in meaning or usage.

Then review any major changes between the two JSON schema versions, and assess if there are any new terms or features we can make use of to improve our ability to validate data against the BODS schema.


## Migrating the data

## Validation and testing

# Update from draft-04 to 2020-12

## Changes

Required:

| From | To | Notes |
| ==== | == | ===== |
| `id` | `$id` | Must resolve to an absolute URI. Should not contain a fragment. |
| `definitions` | `$defs` | |
| `exclusiveMinimum`, `exclusiveMaximum` | changed from bool to number | "wherever one of these would be true before, change the value to the corresponding "minimum" or "maximum" value and remove the "minimum"/"maximum" keyword" |
| `items` | `prefixItems` | |
| `additionalItems` | `items` ||
| `dependencies` | `dependentSchema` and `dependentRequired` | metaschema |


## Additions

Maybe useful:

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