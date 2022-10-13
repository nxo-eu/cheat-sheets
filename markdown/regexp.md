```yaml
title: regexp
category: Others
layout: 2022/sheet
weight: -1
updated: 11-Oct-2022
description: |
  Basic cheatsheets for regular expression
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [RegExp](#RegExp)
	* 1.1. [Character classes](#Characterclasses)
	* 1.2. [Anchors](#Anchors)
	* 1.3. [Escaped characters](#Escapedcharacters)
	* 1.4. [Groups](#Groups)
	* 1.5. [Quantifiers](#Quantifiers)
	* 1.6. [Lookahead & Lookbehind](#LookaheadLookbehind)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

##  1. <a name='RegExp'></a>RegExp

###  1.1. <a name='Characterclasses'></a>Character classes

| Pattern       | Description                              |
| ------------- | ---------------------------------------- |
| `.`           | Any character, except newline            |
| `\w`          | Word                                     |
| `\d`          | Digit                                    |
| `\s`          | Whitespace                               |
| `\W`          | Not word                                 |
| `\D`          | Not digit                                |
| `\S`          | Not whitespace                           |
| `[abc]`       | Any of a, b, or c                        |
| `[a-e]`       | Characters between `a` and `e`           |
| `[1-9]`       | Digit between `1` and `9`                |
| `[[:print:]]` | Any printable character including spaces |
| `[^abc]`      | Any character except `a`, `b` or `c`     |

###  1.2. <a name='Anchors'></a>Anchors

| Pattern | Description             |
| ------- | ----------------------- |
| `\G`    | Start of match          |
| `^`     | Start of string         |
| `$`     | End of string           |
| `\A`    | Start of string         |
| `\Z`    | End of string           |
| `\z`    | Absolute end of string  |
| `\b`    | A word boundry          |
| `\B`    | Non-word boundry        |
| `^abc`  | Start with `abc`        |
| `abc$`  | End with `abc`          |

###  1.3. <a name='Escapedcharacters'></a>Escaped characters

| Pattern    | Description                            |
| ---------- | -------------------------------------- |
| `\. \* \\` | Escape special character used by regex |
| `\t`       | Tab                                    |
| `\n`       | Newline                                |
| `\r`       | Carriage return                        |

###  1.4. <a name='Groups'></a>Groups

| Pattern   | Description                    |
| --------- | ------------------------------ |
| `(abc)`   | Capture group                  |
| `(a|b)`   | Match `a` or `b`               |
| `(?:abc)` | Match `abc`, but don't capture |


###  1.5. <a name='Quantifiers'></a>Quantifiers

| Pattern  | Description           |
| -------- | --------------------- |
| `a*`     | Match 0 or more       |
| `a+`     | Match 1 or more       |
| `a?`     | Match 0 or 1          |
| `a{5}`   | Match exactly 5       |
| `a{,3}`  | Match up to 3         |
| `a{3,}`  | Match 3 or more       |
| `a{1,3}` | Match between 1 and 3 |

###  1.6. <a name='LookaheadLookbehind'></a>Lookahead & Lookbehind

| Pattern      | Description                               |
| ---          | ---                                       |
| `a(?=b)`     | Match `a` in `baby` but not in `bay`      |
| `a(?!b)`     | Match `a` in `Stan` but not in `Stab`     |
| ---          | ---                                       |
| `(?<=a)b`    | Match `b` in `crabs` but not in `cribs`   |
| `(?<!a)b`    | Match `b` in `fib` but not in `fab`       |