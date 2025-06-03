# Validation Specification
BODS contains three types of normative requirement:
- Those which are testable via representation in BODS' JSON schema. (For example: `Interest.type` is a string from the 'Interest type' codelist.)
- Those which are not testable via the schema, but they are testable. (For example: `birthDate` is not a future date.)
- Those which are not computationally testable. (For example, modelling requirements like: "if a person is a beneficial owner of an entity [...] there MUST be a Relationship statement connecting the two which represents the beneficial ownership relationship.")

All normative requirements in BODS which are testable should be documented in the [BODS validation specification](https://docs.google.com/spreadsheets/d/1KTHGSb_ZkCLB9QpjQ891Y_RxvlBJHFEITjOxptaOTAQ/edit?usp=sharing) along with information about how they are tested. Wherever possible validation (testing) is enforced by the JSON schema. Requirements not enforceable by the JSON schema are tested using CoVE (the Data Review Tool), with an 'additional check'.

As BODS is undergoing [test-driven](testing.md) development, the validation specification should be kept up to date. It is the central reference point when updating the Data Review Tool to handle new versions of BODS.

## Adding constraints which need checking in the Data Review Tool
1. Add the constraint to the [Validation specification](https://docs.google.com/spreadsheets/d/1KTHGSb_ZkCLB9QpjQ891Y_RxvlBJHFEITjOxptaOTAQ/edit?gid=220139423#gid=220139423), with 'additional check' in the 'Tested where' column. Indicate in the relevant columns which versions of BODS the check applies to.
2. In a GitHub issue, specify how the check will operate via:
* a description of the check 
* valid and invalid example data
* human-readable error messages for the Data Review Tool 
3. Add a link to the GitHub issue in the notes column (or a temporary 'Development issue' column)

Here is a [previous example of a check issue](https://github.com/openownership/lib-cove-bods/issues/113)

# Data Review Tool 

The Data Review Tool (BODS CoVE) provides human-readable information about whether a series of BODS statements passes validation. That is: whether all the testable requirements of the data standard are met. 

The code spans two repositories:

- [cove-bods](https://github.com/openownership/cove-bods)
- [lib-cove-bods](https://github.com/openownership/lib-cove-bods/tree/master)

## Translations

The Data Review Tool currently is only in English.

However, we know that there will be translations soon and so we are already using the process and workflow.

### When Adding New Strings or altering strings in CoVE BODS

See the "Translations for Developers" section in https://github.com/openownership/cove-bods/blob/master/README.md
