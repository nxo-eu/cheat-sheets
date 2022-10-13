```yaml
title: Markdown
category: Markup
layout: 2017/sheet
prism_languages: [markdown]
updated: 2020-07-01
weight: -1
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Headers](#Headers)
* 2. [Emphasis](#Emphasis)
* 3. [Lists](#Lists)
* 4. [Links](#Links)
* 5. [Images](#Images)
* 6. [Code](#Code)
* 7. [Blockquotes](#Blockquotes)
* 8. [Horizontal line](#Horizontalline)
* 9. [Tables](#Tables)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

###  1. <a name='Headers'></a>Headers

```markdown
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

```markdown
Header 1
========
```

```markdown
Header 2
--------
```

###  2. <a name='Emphasis'></a>Emphasis

```markdown
*italic*
_italic_
```

```markdown
**bold**
__bold__
```

```markdown
***bold italic***
___bold italic___
```

```markdown
~~strikethrough~~
```

```markdown
`code`
```

###  3. <a name='Lists'></a>Lists

```markdown
* Item 1
* Item 2
```

```markdown
- Item 1
- Item 2
```

```markdown
- [ ] Checkbox off
- [x] Checkbox on
```

```markdown
1. Item 1
2. Item 2
```

###  4. <a name='Links'></a>Links

```markdown
[link](http://google.com)
```

```markdown
[link][google]
[google]: http://google.com
```

```markdown
<http://google.com>
```

###  5. <a name='Images'></a>Images

```markdown
![Image alt text](/path/to/img.jpg)
![Image alt text](/path/to/img.jpg "title")
![Image alt text][img]
```

```markdown
[img]: http://foo.com/img.jpg
```

###  6. <a name='Code'></a>Code

```markdown
`inline code`
```

```
    4 space indent
    makes a code block
```

~~~markdown
```
code fences
```
~~~


~~~markdown
```js
codeFences.withLanguage()
```
~~~

###  7. <a name='Blockquotes'></a>Blockquotes

```markdown
> This is
> a blockquote
>
> > Nested
> > Blockquote
```

###  8. <a name='Horizontalline'></a>Horizontal line

```markdown
----
```

```markdown
****
```

###  9. <a name='Tables'></a>Tables

```markdown
| Column 1 Heading | Column 2 Heading |
| ---------------- | ---------------- |
| Some content     | Other content    |
```

```markdown
Column 1 Heading | Column 2 Heading
--- | ---
Some content | Other content
```