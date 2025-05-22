# Validation Specification
All normative and non-normative requirements in the BODS schema should be documented in the [BODS validation specification](https://docs.google.com/spreadsheets/d/1KTHGSb_ZkCLB9QpjQ891Y_RxvlBJHFEITjOxptaOTAQ/edit?usp=sharing) with information about how they are tested. Wherever possible requirements are built directly into the JSON schema. Requirements not testable in JSON are tested using CoVE. Some requirements are not possible to test. 

## Adding new tests
New tests should be documented as a github issue with:
* a description of the test 
* valid and invalid example data
* human-readable error messages for the Data Review Tool 

Here is a [previous example of a test PR](https://github.com/openownership/lib-cove-bods/issues/113)

Implementation of the test will depend on whether it is tested within the schema or using CoVE. 

# Data Review Tool 

The Data Review Tool provides human-readable information about whether a series of BODS statements passes the tests. 

# CoVE Translations

BODS CoVE currently is only in English.

However, we know that there will be translations soon and so we are already using the process and workflow.

## When Adding New Strings or altering strings in CoVE BODS

See the "Translations for Developers" section in https://github.com/openownership/cove-bods/blob/master/README.md
