# BODS Style Guide - #draft

This style guide is a draft to be discussed and not yet implemented across the BODS schema and documentation (as of May 2019, BODS v0.2). It can be used to guide editing and content writing. The Guide is divided into separate, though related, sections: one for the BODS schema and one for the BODS documentation.

## BODS Schema

- Object names and definition entry names to be upper camelCase, e.g. InterestedParty

- Object titles to be uppper case. E.g. 'Interest' or 'Ownership-or-control Statement'.

- In descriptions, properties should be referred to by their property name in backquotes. E.g. \`id\` is required. 

*Codelist codes? Currently most multi-word codes are camelCase (e.g. placeOfBirth). However in the unspecifiedReason and interestType codelists - and poss others - hyphens are used (e.g. information-unknown-to-publisher). We need to introduce some consistency.*

*Markup within descriptions?*

## BODS documentation

restructuredText (.rst) files are used to document BODS. 

- Properties to be referred to by their property name (not title) and marked up as \`\`propertyName\`\`. This can be used to refer to the property and its value. Or it can be used as a shorthand for the property value.

- Objects to be referred to by their title, e.g. '... the Interested Party object has a number of required properties...'

- Statements to be referred to by their titles. e.g. "The details of the company are entered into an Entity Statement"

*How should a code be referred to? By its code or by its title? If by code, this wouldn't be translated. Perhaps use single quotes (e.g. "...use 'placeOfBirth' to refer to an address...") Then translation guidance could instruct translators to retain the code in the text but follow it with the translated code title (e.g. "... utilise 'placeOfBirth' (lieu de naissance) pour faire référence à une adresse...". Similar guidance would work for dealing with property names in translation (see above).* 

*Should we use 'object' or 'block' or even 'component' to refer to JSON objects?*
