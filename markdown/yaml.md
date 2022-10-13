```yaml
title: YAML
date: 12-Oct-2022
tags:
   - config
   - format
categories:
   - Programming
intro: |
    This is a quick reference cheat sheet for understanding and writing YAML format configuration files.
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Introduction](#Introduction)
* 2. [Scalar types](#Scalartypes)
    * 2.1. [↓ Equivalent JSON](#EquivalentJSON)
* 3. [Variables](#Variables)
    * 3.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 4. [Comments](#Comments)
* 5. [Multiline strings](#Multilinestrings)
    * 5.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 6. [Inheritance](#Inheritance)
    * 6.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 7. [Reference](#Reference)
    * 7.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 8. [Folded strings](#Foldedstrings)
    * 8.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 9. [Two Documents](#TwoDocuments)
* 10. [Sequence](#Sequence)
    * 10.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 11. [Mapping](#Mapping)
    * 11.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 12. [Mapping to Sequences](#MappingtoSequences)
    * 12.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 13. [Sequence of Mappings](#SequenceofMappings)
    * 13.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 14. [Sequence of Sequences](#SequenceofSequences)
    * 14.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 15. [Mapping of Mappings](#MappingofMappings)
    * 15.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 16. [Nested Collections](#NestedCollections)
    * 16.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 17. [Unordered Sets](#UnorderedSets)
    * 17.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 18. [Ordered Mappings](#OrderedMappings)
    * 18.1. [↓ Equivalent JSON](#EquivalentJSON-1)
* 19. [Terms](#Terms)
* 20. [Document indicators](#Documentindicators)
* 21. [Collection indicators](#Collectionindicators)
* 22. [Alias indicators](#Aliasindicators)
* 23. [Special keys](#Specialkeys)
* 24. [Scalar indicators](#Scalarindicators)
* 25. [Tag Property (usually unspecified)](#TagPropertyusuallyunspecified)
* 26. [Misc indicators](#Miscindicators)
* 27. [Core types (default automatic tags)](#Coretypesdefaultautomatictags)
* 28. [Escape Codes](#EscapeCodes)
    * 28.1. [Numeric](#Numeric)
    * 28.2. [Protective](#Protective)
    * 28.3. [C](#C)
    * 28.4. [Additional](#Additional)
* 29. [More types](#Moretypes)
* 30. [Language Independent Scalar Types](#LanguageIndependentScalarTypes)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

Getting started 
---------------


###  1. <a name='Introduction'></a>Introduction

[YAML](https://yaml.org/) is a data serialisation language designed to be directly writable and readable by humans

- YAML does not allow the use of tabs
- Must be space between the element parts
- YAML is CASE sensitive
- End your YAML file with the `.yaml` or `.yml` extension
- YAML is a superset of JSON
- Ansible playbooks are YAML files



###  2. <a name='Scalartypes'></a>Scalar types 
```yaml
n1: 1            # integer          
n2: 1.234        # float      

s1: 'abc'        # string        
s2: "abc"        # string           
s3: abc          # string           

b: false         # boolean type 

d: 2015-04-05    # date type
```
####  2.1. <a name='EquivalentJSON'></a>↓ Equivalent JSON
```json 
{
  "n1": 1,
  "n2": 1.234,
  "s1": "abc",
  "s2": "abc",
  "s3": "abc",
  "b": false,
  "d": "2015-04-05"
}
```
Use spaces to indent. There must be space between the element parts.


###  3. <a name='Variables'></a>Variables
```yaml
some_thing: &VAR_NAME foobar
other_thing: *VAR_NAME
```
####  3.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "some_thing": "foobar",
  "other_thing": "foobar"
}
```




###  4. <a name='Comments'></a>Comments
```yaml
# A single line comment example

# block level comment example
# comment line 1
# comment line 2
# comment line 3
```



###  5. <a name='Multilinestrings'></a>Multiline strings
```yaml
description: |
  hello
  world
```
####  5.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{"description": "hello\nworld\n"}
```



###  6. <a name='Inheritance'></a>Inheritance 
```yaml
parent: &defaults
  a: 2
  b: 3

child:
  <<: *defaults
  b: 4
```
####  6.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "parent": {
    "a": 2,
    "b": 3
  },
  "child": {
    "a": 2,
    "b": 4
  }
}
```



###  7. <a name='Reference'></a>Reference 
```yaml
values: &ref
  - Will be
  - reused below
  
other_values:
  i_am_ref: *ref
```
####  7.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "values": [
    "Will be",
    "reused below"
  ],
  "other_values": {
    "i_am_ref": [
      "Will be",
      "reused below"
    ]
  }
}
```


###  8. <a name='Foldedstrings'></a>Folded strings
```yaml
description: >
  hello
  world
```
####  8.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{"description": "hello world\n"}
```



###  9. <a name='TwoDocuments'></a>Two Documents
```yaml
---
document: this is doc 1
---
document: this is doc 2
```
YAML uses `---` to separate directives from document content.






YAML Collections 
-----------

###  10. <a name='Sequence'></a>Sequence
```yaml
- Mark McGwire
- Sammy Sosa
- Ken Griffey
```
####  10.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
[
  "Mark McGwire",
  "Sammy Sosa",
  "Ken Griffey"
]
```


###  11. <a name='Mapping'></a>Mapping
```yaml
hr:  65       # Home runs
avg: 0.278    # Batting average
rbi: 147      # Runs Batted In
```
####  11.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "hr": 65,
  "avg": 0.278,
  "rbi": 147
}
```



###  12. <a name='MappingtoSequences'></a>Mapping to Sequences
```yaml
attributes:
  - a1
  - a2
methods: [getter, setter]
```
####  12.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "attributes": ["a1", "a2"],
  "methods": ["getter", "setter"]
}
```





###  13. <a name='SequenceofMappings'></a>Sequence of Mappings
```yaml
children:
  - name: Jimmy Smith
    age: 15
  - name: Jimmy Smith
    age: 15
  -
    name: Sammy Sosa
    age: 12
```
####  13.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "children": [
    {"name": "Jimmy Smith", "age": 15},
    {"name": "Jimmy Smith", "age": 15},
    {"name": "Sammy Sosa", "age": 12}
  ]
}
```


###  14. <a name='SequenceofSequences'></a>Sequence of Sequences
```yaml
my_sequences:
  - [1, 2, 3]
  - [4, 5, 6]
  -  
    - 7
    - 8
    - 9
    - 0 
```
####  14.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "my_sequences": [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9, 0]
  ]
}
```


###  15. <a name='MappingofMappings'></a>Mapping of Mappings
```yaml
Mark McGwire: {hr: 65, avg: 0.278}
Sammy Sosa: {
    hr: 63,
    avg: 0.288
  }
```
####  15.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "Mark McGwire": {
    "hr": 65,
    "avg": 0.278
  },
  "Sammy Sosa": {
    "hr": 63,
    "avg": 0.288
  }
}
```



###  16. <a name='NestedCollections'></a>Nested Collections
```yaml
Jack:
  id: 1
  name: Franc
  salary: 25000
  hobby:
    - a
    - b
  location: {country: "A", city: "A-A"}
```
####  16.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "Jack": {
    "id": 1,
    "name": "Franc",
    "salary": 25000,
    "hobby": ["a", "b"],
    "location": {
        "country": "A", "city": "A-A"
    }
  }
}
```


###  17. <a name='UnorderedSets'></a>Unordered Sets
```yaml
set1: !!set
  ? one
  ? two
set2: !!set {'one', "two"}
```
####  17.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "set1": {"one": null, "two": null},
  "set2": {"one": null, "two": null}
}
```
Sets are represented as a Mapping where each key is associated with a null value


###  18. <a name='OrderedMappings'></a>Ordered Mappings
```yaml
ordered: !!omap
- Mark McGwire: 65
- Sammy Sosa: 63
- Ken Griffy: 58
```
####  18.1. <a name='EquivalentJSON-1'></a>↓ Equivalent JSON
```json 
{
  "ordered": [
     {"Mark McGwire": 65},
     {"Sammy Sosa": 63},
     {"Ken Griffy": 58}
  ]
}
```






YAML Reference 
--------------

###  19. <a name='Terms'></a>Terms

- Sequences aka arrays or lists
- Scalars aka strings or numbers
- Mappings aka hashes or dictionaries


Based on the YAML.org [refcard](https://yaml.org/refcard.html).


###  20. <a name='Documentindicators'></a>Document indicators

|       |                     |
|-------|---------------------|
| `%`   | Directive indicator |
| `---` | Document header     |
| `...` | Document terminator |



###  21. <a name='Collectionindicators'></a>Collection indicators 

|      |                                 |
|------|---------------------------------|
| `?`  | Key indicator                   |
| `:`  | Value indicator                 |
| `-`  | Nested series entry indicator   |
| `,`  | Separate in-line branch entries |
| `[]` | Surround in-line series branch  |
| `{}` | Surround in-line keyed branch   |


###  22. <a name='Aliasindicators'></a>Alias indicators

|     |                 |
|-----|-----------------|
| `&` | Anchor property |
| `*` | Alias indicator |


###  23. <a name='Specialkeys'></a>Special keys

|      |                                 |
|------|---------------------------------|
| `=`  | Default "value" mapping key     |
| `<<` | Merge keys from another mapping |


###  24. <a name='Scalarindicators'></a>Scalar indicators

|       |                                                                                              |
|-------|----------------------------------------------------------------------------------------------|
| `''`  | Surround in-line unescaped scalar                                                            |
| `"`   | Surround in-line escaped scalar                                                              |
| `|`   | Block scalar indicator                                                                       |
| `>`   | Folded scalar indicator                                                                      |
| `-`   | Strip chomp modifier (`|-` or `>-`)                                                          |
| `+`   | Keep chomp modifier (`|+` or `>+`)                                                           |
| `1-9` | Explicit indentation modifier (`|1` or `>2`). <br/> Modifiers can be combined (`|2-`, `>+1`) |


###  25. <a name='TagPropertyusuallyunspecified'></a>Tag Property (usually unspecified) 
|          |                                                             |
|----------|-------------------------------------------------------------|
| `none`   | Unspecified tag (automatically resolved by application)     |
| `!`      | Non-specific tag (by default, `!!map`/`!!seq`/`!!str`)      |
| `!foo`   | Primary (by convention, means a local `!foo` tag)           |
| `!!foo`  | Secondary (by convention, means `tag:yaml.org,2002:foo`)    |
| `!h!foo` | Requires `%TAG !h! <prefix>` (and then means `<prefix>foo`) |
| `!<foo>` | Verbatim tag (always means `foo`)                           |

###  26. <a name='Miscindicators'></a>Misc indicators

|     |                             |
|-----|-----------------------------|
| `#` | Throwaway comment indicator |
| <code>\`@</code> | Both reserved for future use |


###  27. <a name='Coretypesdefaultautomatictags'></a>Core types (default automatic tags) 

|         |                                          |
|---------|------------------------------------------|
| `!!map` | `{Hash table, dictionary, mapping}`      |
| `!!seq` | `{List, array, tuple, vector, sequence}` |
| `!!str` | Unicode string                           |



###  28. <a name='EscapeCodes'></a>Escape Codes 

####  28.1. <a name='Numeric'></a>Numeric

- `\x12` (8-bit)
- `\u1234` (16-bit)
- `\U00102030` (32-bit)
  

####  28.2. <a name='Protective'></a>Protective

- `\\` (\\)
- `\"` (")
- `\ ` ( )
- `\<TAB>` (TAB)
  

####  28.3. <a name='C'></a>C
- `\0` (NUL)
- `\a` (BEL)
- `\b` (BS)
- `\f` (FF)
- `\n` (LF)
- `\r` (CR)
- `\t` (TAB)
- `\v` (VTAB)
  

####  28.4. <a name='Additional'></a>Additional

- `\e` (ESC)
- `\_` (NBSP)
- `\N` (NEL)
- `\L` (LS)
- `\P` (PS)
  
  
###  29. <a name='Moretypes'></a>More types

|          |                             |
|----------|-----------------------------|
| `!!set`  | `{cherries, plums, apples}` |
| `!!omap` | `[one: 1, two: 2]`          |



###  30. <a name='LanguageIndependentScalarTypes'></a>Language Independent Scalar Types 

|                           |                                            |
|---------------------------|--------------------------------------------|
| `{~, null}`               | Null (no value).                           |
| `[1234, 0x4D2, 02333]`    | [Decimal int, Hexadecimal int, Octal int]  |
| `[1_230.15, 12.3015e+02]` | [Fixed float, Exponential float]           |
| `[.inf, -.Inf, .NAN]`     | [Infinity (float), Negative, Not a number] |
| `{Y, true, Yes, ON}`      | Boolean true                               |
| `{n, FALSE, No, off}`     | Boolean false                              |



Also see 
--------
- [YAML Reference Card](https://yaml.org/refcard.html) _(yaml.org)_
- [Learn X in Y minutes](https://learnxinyminutes.com/docs/yaml/) _(learnxinyminutes.com)_
- [YAML lint online](http://www.yamllint.com/) _(yamllint.com)_
