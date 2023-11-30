
The Future of Data Systems  
If a thing be ordained to another as to its end, its last end cannot consist in the preservation  
of its being. Hence a captain does not intend as a last end, the preservation of the ship  
entrusted to him, since a ship is ordained to something else as its end, viz. to navigation.  
(Often quoted as: If the highest aim of a captain was the preserve his ship, he would keep it  
in port forever.)  
—St. Thomas Aquinas, Summa Theologica (1265–1274)

A partitioned system with secondary indexes either needs to send writes to multiple partitions (if the index is term-partitioned) or send reads to all partitions (if the index is document-partitioned). Such cross-partition communication is also most reliable and scalable if the index is maintained asynchronously

How does stream processing support derived data views?
Stream processing allows changes in the input to be reflected in derived views with low delay

How does batch processing support derived data views?
batch processing allows large amounts of accumulated historical data to be reprocessed in order to derive new views onto an existing dataset.

How does reprocessing data allow in a way schema migration?
Batch & stream processing can be used to produce a new derived data view, effectively a schema change of another derived view. Derived views allow gradual evolution of your data schema 

What is a lambda architecture?
- incoming data should be recorded by appending immutable events to an always-growing dataset, similarly to event sourcing
- from the events read-optimized views are derived
- run batch processing system (like Hadoop) & streaming processing system (like Storm) in parallel
- both systems process all events
- stream processing updates derived views quickly and batch process later updates the derived view with more accurate data


What is a federated database?
(AKA polystore)
- unified query interface to a wide variety of underlying storage engines and processing methods

--- Anki Cards Needed ---

What is an unbundled database?

pg 521