
rolling upgrade/staged rollout - deploying the new version of a software a few nodes at a time, checking whether the new version is running smoothly, and gradually working your way through all the nodes.

backward compatibility - Newer code can read data that was written by older code.

Forward compatibility - Older code can read data that was written by newer code.

Programs usually work with data in (at least) two different representations:
1. In memory, data is kept in objects, structs, lists, arrays, hash tables, trees, and so
on. These data structures are optimized for efficient access and manipulation by
the CPU (typically using pointers).
2. When you want to write data to a file or send it over the network, you have to
encode it as some kind of self-contained sequence of bytes (for example, a JSON
document). Since a pointer wouldn’t make sense to any other process, this sequence-of-bytes representation looks quite different from the data structures
that are normally used in memory

Thus, we need some kind of translation between the two representations. The translation
from the in-memory representation to a byte sequence is called encoding (also
known as serialization or marshalling), and the reverse is called decoding (parsing,
deserialization, unmarshalling).

Encoding - also known as serialization is the process of translating an in memory representation of data into a byte sequence.

Decoding - also known as deserialization is the process of translating a byte sequence to an in memory representation of the data

## Encoding Variants

### Programming Language Specific Encoding

Generally programming languages will have built in encoding/decoding functions that encode/decode in their own unique way. This is not recommended because the encoded data cannot be read by applications running off other programming languages. Also programming language decoding usually instantiate arbitrary classes when reading in the bytes so a malicious actor could send a encoded object to be decoded that executes malicious code.

### Human Readable Encoding Formats

JSON, XML, CSV are human readable formats for data encoding/decoding.

Pros: 
- human readable
- easy to work with
- JSON & XML have good Unicode character support
Cons:
- XML & CSV can't differentiate numbers and strings when it comes to a set of digits
- JSON cannot distinguish numbers from floating point numbers and their precision
- JSON & XML do no support binary string although a hacky work around is encoding binary data as text using Base64. The Base64 solution is hacking and increases data size by 33%

In most situations, as long as people
agree on what the format is, it often doesn’t matter how pretty or efficient the format
is. The difficulty of getting different organizations to agree on anything outweighs
most other concerns.

### Binary Encoding

There are binary encoding variants of JSON and XML but none have seen wide adoption and generally do not have enough of a storage saving result that outweighs the JSON/XML human readability

Thrift (meta) & Protobuf (Google) are 2 popular open source binary encoding frameworks which come with code generation tools for various languages.

![[Pasted image 20231031125249.png]]

One of the main encoding efficiencies is the use of tag numbers. Each field is given a tag number marking its position in the schema. This number is encoded, not the actual name of the field. 

```protobuf
message Person {
	required string user_name = 1;
	optional int64 favorite_number = 2;
	repeated string interests = 3;
}
```

Protobuf & Thrift tagging system both support forward and backward compatibility. 

**Apache Avro** is another binary encoding type that instead of using number tags it simply just concatenates the bytes of each value together making it the least amount of bytes in total compared to Protobuf or Thrift. To maintain backward/forward compatibility it sends the writers schema with the encoding data which is used to match the encoded fields with the reads schema. One of its main advantages over Protobuf/Thrift is that since it does not have number tags it is friendlier to dynamically generated schemas.

![[Pasted image 20231031131255.png]]

So, we can see that although textual data formats such as JSON, XML, and CSV are
widespread, binary encodings based on schemas are also a viable option. They have a
number of nice properties:
• They can be much more compact than the various “binary JSON” variants, since
they can omit field names from the encoded data.
• The schema is a valuable form of documentation, and because the schema is
required for decoding, you can be sure that it is up to date (whereas manually
maintained documentation may easily diverge from reality).
• Keeping a database of schemas allows you to check forward and backward compatibility
of schema changes, before anything is deployed.
• For users of statically typed programming languages, the ability to generate code
from the schema is useful, since it enables type checking at compile time.
In summary, schema evolution allows the same kind of flexibility as schemaless/
schema-on-read JSON databases provide (see “Schema flexibility in the document
model” on page 39), while also providing better guarantees about your data and better
tooling.

## Data Flows 

When it comes to forward/backward compatibility for maintaining database integrity when new and old versions of apps are updating database records it is important to note and think about handling that in the application logic so that no data is lost during translation. For example, if an old version updates a record that contains a new field it is not aware of it should not lose the new field during data translation.

![[Pasted image 20231031134106.png]]

Applications update and evolve quickly, data in your database does not and old data may remain for a long time, therefore there is a saying, *data outlives code*

Rewriting (migrating) data into a new schema is possible bit it is an expensive operation to do.

## REST & RPC

In the client server model where the server exposes some API to be called by the client we call that API a service. When HTTP is used as the underlying protocol for talking to a service it is called a *web service*. 

REST is not a protocol, but rather a design philosophy that builds upon the principles
of HTTP. It emphasizes simple data formats, using URLs for identifying
resources and using HTTP features for cache control, authentication, and content
type negotiation. REST has been gaining popularity compared to SOAP, at least in
the context of cross-organizational service integration, and is often associated
with microservices. An API designed according to the principles of REST is
called RESTful.

SOAP is an XML-based protocol for making network API requests.vii
Although it is most commonly used over HTTP, it aims to be independent from
HTTP and avoids using most HTTP features. Instead, it comes with a sprawling and
complex multitude of related standards (the web service framework, known as WS-*)
that add various features 

The API of a SOAP web service is described using an XML-based language called the
Web Services Description Language, or WSDL. WSDL enables code generation so
that a client can access a remote service using local classes and method calls (which
are encoded to XML messages and decoded again by the framework). This is useful in
statically typed programming languages, but less so in dynamically typed ones (see
“Code generation and dynamically typed languages” on page 127).

As WSDL is not designed to be human-readable, and as SOAP messages are often too
complex to construct manually, users of SOAP rely heavily on tool support, code
generation, and IDEs. For users of programming languages that are not supported
by SOAP vendors, integration with SOAP services is difficult

RPC - (remote procedure call) The RPC model tries to make a request to a remote network service look the same as calling a function or method in your programming language, within the same process (this abstraction is called location transparency). There are problems with this because it adds coupling between the language and the network request itself. Some datatypes may function differently in different languages which can be problematic for RPC. Network request differ greatly from how functions work in general so that can make working with it difficult since a lot of different things can happen to network request which should be debugged differently then a normal function. [pg134]

There are still good applications of RPC since gRPC is used for Protobuf a lot, gRPC supports *streams*, multiple requests/responses instead of one of each. Some of the frameworks support service discovery, allowing a client to find out at which IP address and port number it can find a particular service

There is no agreement on how API versioning should work (i.e., how a client can
indicate which version of the API it wants to use [48]). For RESTful APIs, common
approaches are to use a version number in the URL or in the HTTP Accept header.

## Message Passing Data Flow

A message broker is an intermediatory between a client and server. The client and server generally are services themselves that are communicating.  Popular open source Message Brokers are RabbitMQ & Apache Kafka.

The detailed delivery semantics vary by implementation and configuration, but in
general, message brokers are used as follows: one process sends a message to a named
queue or topic, and the broker ensures that the message is delivered to one or more
consumers of or subscribers to that queue or topic. There can be many producers and
many consumers on the same topic

A topic provides only one-way dataflow. However, a consumer may itself publish
messages to another topic (so you can chain them together, as we shall see in Chapter
11), or to a reply queue that is consumed by the sender of the original message
(allowing a request/response dataflow, similar to RPC).

### Distributed Actor Frameworks 

pg138-139

Actor Model - a programming model for concurrency in a single process. Rather
than dealing directly with threads (and the associated problems of race conditions,
locking, and deadlock), logic is encapsulated in actors. Each actor typically represents
one client or entity, it may have some local state (which is not shared with any other
actor), and it communicates with other actors by sending and receiving asynchronous
messages. Message delivery is not guaranteed: in certain error scenarios, messages
will be lost. Since each actor processes only one message at a time, it doesn’t
need to worry about threads, and each actor can be scheduled independently by the
framework.

distributed actor frameworks - programming model is used to scale an application
across multiple nodes. The same message-passing mechanism is used, no matter
whether the sender and recipient are on the same node or different nodes. If they are
on different nodes, the message is transparently encoded into a byte sequence, sent
over the network, and decoded on the other side

