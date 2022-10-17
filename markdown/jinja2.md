```yaml
title: Jinja
category: Python
layout: 2022/sheet
```
{% raw %}

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Jinja2](#Jinja2)
	* 1.1. [Basic usage](#Basicusage)
	* 1.2. [Control structures](#Controlstructures)
	* 1.3. [Whitespace trimming](#Whitespacetrimming)
	* 1.4. [Special blocks](#Specialblocks)
	* 1.5. [Inheritance](#Inheritance)
		* 1.5.1. [shared.html](#shared.html)
		* 1.5.2. [home.html](#home.html)
* 2. [Library](#Library)
	* 2.1. [Basic usage](#Basicusage-1)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

##  1. <a name='Jinja2'></a>Jinja2

###  1.1. <a name='Basicusage'></a>Basic usage

```jinja2
- variable x has content: {{ x }}
- expression: {{ x + 1 }}
- escaped for HTML: {{ x | e }}
```

###  1.2. <a name='Controlstructures'></a>Control structures

```jinja2
{% for x in range(5) %}
    {% if x % 2 == 0 %}
        {{ x }} is even!
    {% else %}
        {{ x }} is odd!
    {% endif %}
{% endfor %}
```

###  1.3. <a name='Whitespacetrimming'></a>Whitespace trimming

```jinja2
these are
{{ "three" }}
lines.

this is conc
{{- "at" -}}
enated.
```

###  1.4. <a name='Specialblocks'></a>Special blocks

```jinja2
{% filter e %}{% endraw %}
{ {%- if 0 -%}{%- endif -%} % raw %}
{%- raw -%}
    This is a raw block where {{nothing is evaluated}}
    {% not even this %}
    and <html is escaped> too with "e" filter
{% endraw %}
{ {%- if 0 -%}{%- endif -%} % endraw %}{% raw %}
{% endfilter %}

{% macro myfunc(x) %}
    this is a reusable macro, with arguments: {{x}}
{% endmacro %}

{{ myfunc(42) }}

{#
this is a comment
#}
```


###  1.5. <a name='Inheritance'></a>Inheritance

####  1.5.1. <a name='shared.html'></a>shared.html

```html
<html>
  <head>
    <title>{%block title %}{% endblock %}</title>
  </head>
  <body>
    <header><h1>{% block title %}{% endblock %}</h1></header>
    <main>{% block content %}{% endblock %}</main>
  </body>
</html>
```

####  1.5.2. <a name='home.html'></a>home.html

```jinja2
{% extends "shared.html" %}
{% block title %}Welcome to my site{% endblock %}
{% block content %}
This is the body
{% endblock %}
```

##  2. <a name='Library'></a>Library

###  2.1. <a name='Basicusage-1'></a>Basic usage

```python
from jinja2 import Template
template = Template('Hello {{ name }}!')
template.render(name='John Doe') == u'Hello John Doe!'
```
{% endraw %}
