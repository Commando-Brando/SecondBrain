
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


### When To Use Which Model

**Document** - use whenever your application mostly has one-to-many relationships (tree-structured data) or no relationships between records.

**Relational** - when there are clear relationships in data and many-to-one relationships and/or simple many-to-many relationships

**Graph** - when there are many many-to-many relationships 
	Examples:
	- Social Graphs: modeling people who know each other or are friends or followers
	- Web Graph: vertices are web pages and edges indicate HTML links to other pages
	- Road or rail networks

>Facebook maintains a single graph with many different types of vertices and edges: vertices represent people, locations, events, check-ins, and comments made by users; edges indicate which people are friends with each other, which check-in happened in which location, who commented on which post, who attended which event, and so on.

## Graph Models

### Property Graph

- vertices & edges are objects that each contain their own JSON properties
- any vertices can be connected to another via an edge that is bidirectional
- edges have labels representing the type of relationship
- allows you to store different kinds of data in a single graph
- edges stored in one table and vertices in another, edges have a `tail_vertex` & `head_vertex`columns
- can use Cypher declarative language or SQL to query graph database (prefer Cypher)

### Triple-Stores and SPARQL

Triple stores are very similar to property graphs.
In a triple-store, all information is stored in the form of very simple three-part statements: (subject, predicate, object). For example, in the triple `(Jim, likes, bananas)`, Jim is the subject, likes is the predicate (verb), and bananas is the object.

The subject of a triple is equivalent to a vertex in a graph. The object is one of two things:

1. A value in a primitive datatype, such as a string or a number. In that case, the predicate and object of the triple are equivalent to the key and value of a property on the subject vertex. For example, `(Lucy, age, 33)` is like a vertex Lucy with properties `{"age":33}`.
2. Another vertex in the graph. In that case, the predicate is an edge in the graph, the subject is the tail vertex, and the object is the head vertex. For example, in `(Lucy, marriedTo, Alain)` the subject and object Lucy and Alain are both vertices, and the predicate `marriedTo` is the label of the edge that connects them.

>The `semantic web` is fundamentally a simple and reasonable idea: websites already publish information as text and pictures for humans to read, so why don’t they also publish information as machine-readable data for computers to read?

SPARQL is a query language for triples.