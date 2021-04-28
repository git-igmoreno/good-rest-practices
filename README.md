# Good practices for API design


## Use Resource Oriented Design

**Resource Oriented Design** consists on three key concepts:
- **Resource**: Represents a piece of data. For example a **Book** 
- **Collection**: Represents a group of resources. For example a **list of Books**
- **URL**: Especifies location of a resource o collection. For example: **/books**

## Use kebab-case for URLs

To get the collection of all editorial contracts:
**Bad**: 
```/editorialContracts or /editorial_contracts```
**Good**:
```/editorial-contracts```

## Use camelCase for Parameters

To get the collection of all books of an author:
**Bad**:
```/books/{author-id} or /books/author_id```
**Good**:
```/books/{authorId}```

## Use plural name to reference collections
To get the collection of authors:
**Bad**:
```GET /author or GET /Author```
**Good**:
```GET /authors```

## URL starts with a Collection, and ends wit an Identifier
To get book pirces of an editorial:
**Bad**:
```GET /author/:authorId/:bookprice/books ```
**Good**:
```GET /Books/:bookId or GET /Authors/authorId```

## Don't use verbs on your URL to access Resources
Verbs are intrinsically determined by HTTP methods, don't need to clarify it twice:
**Bad**:
```POST /updateBook/{bookId}```
**Good**:
```PUT /book/{bookId} or PATCH /book/{bookId}```

## Use verbs on your URL to call Operations
Something you need to execute a server-side operation. In that case is correct to use verbs:
**Good**:
```POST /books/:bookId/promote```

## Use camelCase on JSON properties
As convention:
**Bad**:
```
	{
		"book_title": "",
		"author_notes":[]
	}
```
**Good**:
```
	{
		"bookTitle": "",
		"authorNotes":[]
	}
```

## Provide service monitoring URLs
A complete RESTful service must provide at least these two monitoring URLS:

**/health**: Must response with a ```200 OK```  status code.

**/version**: Must response with the API version number.

You can also provide **/metrics**, **/debug** (for testing) and **/status** endpoints.

## Avoid exposing underlying architecture
Use proper resource and collection names, avoid to expose technical or implementation inner issues.
**Bad**:
```table_books```
**Good**:
```books```

## API version as simple ordinal
API version should be v1, v2. Version must be specified at the left of the URL parameters.

## Include resources count in REST responses
**Bad**:
```
	{
		books:[]
	}
```
**Good**:
```
	{
		books:[],
		total: 0
	}
```

## Allow Offset and Pagination parameters
Always accept ````limit```, ```offset``` or ```page``` parameters to narrow down your API responses
