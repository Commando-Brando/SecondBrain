
If there are strings that a lot of users set, for example their city, then it is better in the database to represent the city as an ID linked to another table of cities and not let them each type in a string themselves but offer them a selection. There are a variety of reasons but from a normalization standpoint if a city name changes or people want to do a lookup of other users based on location having this allows you to only need to change the city name in one place & also easily query based on city.

## Document Model

**Schema-On-Read** - when the schema is defined when the data is read from the data source. For example, documents have no set schema but when the data is read into an object it must conform to the objects schema. It is advantageous when:
- here are many different types of objects, and it is not practical to put each type of object in its own table.
- The structure of the data is determined by external systems over which you have no control and which may change at any time.
- locality of data is important and documents are not large. There does not need to be joins if all the data is local to each document`

## Relational Model

**Schema-On-Write** - when the schema is defined when the data is written for example, an RDBMS defines its schema by its table structures and so enforces it when data is written


## Declarative vs Imperative Datastore Querying

Declarative coding is advantageous sometimes because the code may be simpler and optimizations can be done within the abstraction so you don't need to change your code to benefit from such an optimization.

>A usability problem with MapReduce is that you have to write two carefully coordinated JavaScript functions, which is often harder than writing a single query. Moreover, a declarative query language offers more opportunities for a query optimizer to improve the performance of a query. For these reasons, MongoDB 2.2 added support for a declarative query language called the aggregation pipeline [9]. In this language, the same shark-counting query looks like this:
```js
db.observations.aggregate([
	{ $match: { family: "Sharks" } },
	{ $group: {
		_id: {
			year: { $year: "$observationTimestamp" },
			month: { $month: "$observationTimestamp" }
		},
		totalAnimals: { $sum: "$numAnimals" }
	} }
]);
```
>The aggregation pipeline language is similar in expressiveness to a subset of SQL, but it uses a JSON-based syntax rather than SQL’s English-sentence-style syntax; the difference is perhaps a matter of taste. The moral of the story is that a NoSQL system may find itself accidentally reinventing SQL, albeit in disguise