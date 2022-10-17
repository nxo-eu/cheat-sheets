```yaml
title: GraphQL
layout: 2022/sheet
updated: 17-Oct-2022
category: API
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Intro](#Intro)
* 2. [Queries](#Queries)
	* 2.1. [Basic query](#Basicquery)
		* 2.1.1. [Response](#Response)
	* 2.2. [Nesting](#Nesting)
		* 2.2.1. [Response](#Response-1)
	* 2.3. [Lists](#Lists)
		* 2.3.1. [Response](#Response-1)
	* 2.4. [Lookups](#Lookups)
		* 2.4.1. [Response](#Response-1)
	* 2.5. [Aliases](#Aliases)
		* 2.5.1. [Response](#Response-1)
	* 2.6. [Operation names and variables](#Operationnamesandvariables)
		* 2.6.1. [Query](#Query)
		* 2.6.2. [Variables](#Variables)
	* 2.7. [Mutations](#Mutations)
		* 2.7.1. [Query](#Query-1)
		* 2.7.2. [Variables](#Variables-1)
		* 2.7.3. [Response](#Response-1)
	* 2.8. [Multiple types](#Multipletypes)
		* 2.8.1. [GET](#GET)
		* 2.8.2. [POST](#POST)
	* 2.9. [Basic schemas](#Basicschemas)
	* 2.10. [Built in types](#Builtintypes)
		* 2.10.1. [Scalar types](#Scalartypes)
		* 2.10.2. [Type definitions](#Typedefinitions)
		* 2.10.3. [Type modifiers](#Typemodifiers)
	* 2.11. [Mutations](#Mutations-1)
	* 2.12. [Interfaces](#Interfaces)
	* 2.13. [Enums](#Enums)
	* 2.14. [Unions](#Unions)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

##  1. <a name='Intro'></a>Intro

GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

##  2. <a name='Queries'></a>Queries

###  2.1. <a name='Basicquery'></a>Basic query

```js
{ status }
```

####  2.1.1. <a name='Response'></a>Response

```js
{ status: 'available' }
```

###  2.2. <a name='Nesting'></a>Nesting

```js
{ hero { name height } }
```

####  2.2.1. <a name='Response-1'></a>Response

```js
{ hero:
    { name: "Luke Skywalker",
      height: 1.74 } }
```

###  2.3. <a name='Lists'></a>Lists

```js
{ friends { name } }
```

####  2.3.1. <a name='Response-1'></a>Response

```js
{ friends:
    [ { name: "Luke Skywalker" },
      { name: "Han Solo" },
      { name: "R2D2" } ] }
```

GraphQL queries look the same for both single items or lists of items.

###  2.4. <a name='Lookups'></a>Lookups

```js
{
  hero(id: "1000") { id name }
}
```

####  2.4.1. <a name='Response-1'></a>Response

```js
{ hero:
    { id: "1000",
    { name: "Luke Skywalker" } }
```

###  2.5. <a name='Aliases'></a>Aliases

```js
{
  luke: hero(id: "1000") { name }
  han: hero(id: "1001") { name }
}
```

####  2.5.1. <a name='Response-1'></a>Response

```js
{ luke:
    { name: "Luke Skywalker" },
    han:
    { name: "Han Solo" } }
```

###  2.6. <a name='Operationnamesandvariables'></a>Operation names and variables

####  2.6.1. <a name='Query'></a>Query
```js
query FindHero($id: String!) {
  hero(id: $id) { name }
}
```

Just to make things less ambiguous. Also, to use variables, you need an operation name.

####  2.6.2. <a name='Variables'></a>Variables

```js
{ id: '1000' }
```

###  2.7. <a name='Mutations'></a>Mutations

####  2.7.1. <a name='Query-1'></a>Query

```js
{ createReview($review) { id } }
```

####  2.7.2. <a name='Variables-1'></a>Variables

```js
{ review: { stars: 5 } }
```

####  2.7.3. <a name='Response-1'></a>Response

```js
{ createReview: { id: 5291 } }
```

Mutations are just fields that do something when queried.

###  2.8. <a name='Multipletypes'></a>Multiple types

```js
{
  search(q: "john") {
    id
    ... on User { name }
    ... on Comment { body author { name } }
  }
}
```

Great for searching.


Over HTTP
---------

####  2.8.1. <a name='GET'></a>GET

```js
fetch('http://myapi/graphql?query={ me { name } }')
```

####  2.8.2. <a name='POST'></a>POST

```js
fetch('http://myapi/graphql', {
  body: JSON.stringify({
    query: '...',
    operationName: '...',
    variables: { ... }
  })
})
```

Schema
------

###  2.9. <a name='Basicschemas'></a>Basic schemas

```js
type Query {
  me: User
  users(limit: Int): [User]
}

type User {
  id: ID!
  name: String
}
```

See: [sogko/graphql-shorthand-notation-cheat-sheet](https://raw.githubusercontent.com/sogko/graphql-shorthand-notation-cheat-sheet/master/graphql-shorthand-notation-cheat-sheet.png)

###  2.10. <a name='Builtintypes'></a>Built in types

####  2.10.1. <a name='Scalartypes'></a>Scalar types

| Name | Description |
|---|---|
| `Int` | Integer |
| `Float` | Float |
| `String` | String |
| `Boolean` | Boolean |
| `ID` | ID |

####  2.10.2. <a name='Typedefinitions'></a>Type definitions

| Name | Description |
|---|---|
| `scalar` | Scalar type |
| `type` | Object type |
| `interface` | Interface type |
| `union` | Union type |
| `enum` | Enumerable type |
| `input` | Input object type |

####  2.10.3. <a name='Typemodifiers'></a>Type modifiers

| Name | Description |
|---|---|
| `String` | Nullable string |
| `String!` | Required string |
| `[String]` | List of strings |
| `[String]!` | Required list of strings |
| `[String!]!` | Required list of required strings |

###  2.11. <a name='Mutations-1'></a>Mutations

```js
type Mutation {
  users(params: ListUsersInput) [User]!
}
```

###  2.12. <a name='Interfaces'></a>Interfaces

```js
interface Entity {
  id: ID!
}

type User implements Entity {
  id: ID!
  name: String
}
```

###  2.13. <a name='Enums'></a>Enums

```js
enum DIRECTION {
  LEFT
  RIGHT
}

type Root {
  direction: DIRECTION!
}
```

###  2.14. <a name='Unions'></a>Unions

```js
type Artist { ··· }
type Album { ··· }

union Result = Artist | Album

type Query {
  search(q: String) [Result]
}
```

References
----------

- <http://graphql.org/learn/queries/>
- <http://graphql.org/learn/serving-over-http/>

