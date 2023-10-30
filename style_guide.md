# BODS Style Guide - #WIP

This style guide is a draft not yet implemented across the BODS schema and documentation (as of October 2023 BODS 0.3). It can be used to guide editing and content writing.

## Common Conventions

### Readability 
We try to write clear, concise documentation, using plain English where possible. 

These tools can help with this:
- [Hemingway editor](https://hemingwayapp.com/)
- [Grammarly](https://www.grammarly.com/)
- [Readability tools](https://www.webfx.com/tools/read-able/)

### Spelling 
Use English spelling:
- 'organisation' not 'organization'
- 'standardised' not 'standardized'
- 'modelling' not 'modeling'

### Word choice
- use 'person' instead of using 'individual' as a noun. You can use 'natural person' to avoid confusion with 'legal person'
- use 'entity,' 'legal person' or specific descriptors like 'trust' to describe legal entities
- 'changelog' not 'change-log,' 'change log,' or 'changeLog'
- 'codelist' not 'code-list,' 'code list' or 'codeList'
- 'politically exposed' not 'politically-exposed'
- 'free text' not 'free-text'
- do not use constructions like “person(s)”, “the supplier (or suppliers)”, or 'one or more persons'. The plural is fine, “persons.”
- refer to JSON objects as 'objects' not 'blocks' or 'components' 

### Names and titles 
'Names' refer to JSON keys, codelists and codelist entries used in the schema.  

Names:
- are formatted using camelCase (e.g 'interestedParty', 'entityType', 'identifiers')
- do not contain spaces or punctuation
- are not translated into languages other than English

'Titles' are the way that a name is referred to in the documentation. (e.g 'Use the Statement Fragment Pointer to describe...')

Titles:
- have all words capitalised
- have spaces between words
- are translated into languages other than English

### Normative Statements
Normative statements MUST:
- be constructed using the keywords defined in [RFC2119](https://datatracker.ietf.org/doc/html/rfc2119) 
- have capitalised keywords to distinguish from those words being used in a non-normative statement

Non-normative statements:
- MAY use the same keywords as normative statements
- MUST format normative keywords in lower case (e.g 'Implementers should be aware that future changes are anticipated')

## Schema style guide

### Duplication
Avoid multiple representations of the same fact where possible. A user should, ideally, have a single way of answering a given question. Having multiple representations of the same fact also introduces the possibility of inconsistent values.

### Field and code descriptions 
The first sentence of a description should:
- be a statement not a question. E.g for beneficialOwnershipOrControl - 'Whether the statement asserts this relationship as beneficial ownership or control' not 'Does this statement assert this as a beneficial ownership or control interest?'
- be written in a neutral voice, not for a specific audience. E.g for 'foundingDate' - 'When the entity was founded, in ISO 8601 format' not 'When the entity was founded, please provide this in ISO 8601 format'

Subsequent sentences may provide information or guidance to assist publishers to use the field effectively or users to interpret the field effectively. Guidance sentences should be grounded in clear user needs and implementation experience of common pitfalls or errors.

Descriptions with a link to a codelist should be phrased as - '\<description\>, using the \<name\> codelist.'

Descriptions should also:
- refer to names using backquotes E.g. "\`id\` is required" (*wip - why backquotes specifically?*) 
- refer to values, whether example free text strings or values from a codelist, using single quotes. E.g. "the given name for Johann Sebastian Bach is 'Johann Sebastian'"
- use plain text only, without markup (eg. no \[Markdown\](https://en.wikipedia.org/wiki/Markdown) or similar syntax)
- place URLs in brackets by the appropriate word or phrase or at the end of the sentence

Descriptions should not:
- include duplications of the codelist as part of the description
- link to external websites
- only restate the title or name E.g 'Address type' - 'The address type'
- explicity state whether a field is required or optional (this is indicated by an asterisk)
- declare the type of the field (this is indicated above the description) 

Assuming the rest of the guidance is followed, it is recommended to start the description with:
- “Whether”, for a boolean field.
- “The” with a plural noun phrase, for the description of an array of strings.

  
### 

## Documentation style guide 

### Bulleted lists
When using bulleted lists you should:
- start with a lead in line, followed by a colon
- use lower case at the start of each bullet
- do not put semicolons or full stops at the end of bullets
- do not put or/and at the end of bullets
- try to have one sentence per bullet

### Restructured text files 

[restructuredText (.rst) files](https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html) are used to document BODS. 

- Properties to be referred to by their property name (not title) and marked up as \`\`propertyName\`\`. This can be used to refer to the property and its value. Or it can be used as a shorthand for the property value.

- Objects to be referred to by their title, e.g. '... the Interested Party object has a number of required properties...'

- Statements to be referred to by their titles. e.g. "The details of the company are entered into an Entity Statement"

### Embeddeding schema objects

We use various plugins to embed schema and codelist elements in dynamic ways.

[JSONValue](https://github.com/openownership/data-standard/blob/3766d9a55b61d2b1b5f27c37dfd5fd24f1cc9884/docs/conf.py#L186) (in the docs `conf.py`) to pull out the value of one key in the JSON, e.g.:

```
.. json-value:: ../_build_schema/components.json
   :pointer: /definitions/Address/description
```

![Screenshot: Address description from the schema rendered as a paragraph](screenshots/docs/embed_jsonpointer.png)

[JSONSchema](https://github.com/OpenDataServices/sphinxcontrib-jsonschema) (a Sphinx extension) to make a table of multiple key-value pairs from the JSON, e.g.:

```
.. jsonschema:: ../_build_schema/components.json
   :pointer: /definitions/Address
   :externallinks: {"type":{"url":"#addresstype","text":"Codelists"}}
```

![Screenshot: Address attributes and properties from the schema rendered as a table](screenshots/docs/embed_jsonschema.png)

[CSVTable](http://docutils.sourceforge.net/docs/ref/rst/directives.html#csv-table) (a builtin Sphinx directive) to make a table from codelist csv files, e.g.:

```
.. csv-table::
   :header-rows: 1
   :class: codelist-table
   :file: ../_build_schema/codelists/addressType.csv
```

![Screenshot: addressTypes codelist rendered as a table](screenshots/docs/embed_codelist.png)


### RST usage

**DO NOT** use this directive to embed HTML elements in the docs. (Encompassed strings will not be picked up for translation.)

```
.. raw:: html

    <h2>
        Background
    </h2>
```


## Reference Page 
The reference page should be ordered:
- objects
- codelists

These sections should be ordered alphabetically. 

Use titles not names for the subheadings of the objects and codelists sections.

