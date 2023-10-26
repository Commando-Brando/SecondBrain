
>Wer Ordnung hält, ist nur zu faul zum Suchen.
 If you keep things tidily ordered, you’re just too lazy to go searching.) 
 —German proverb

We can think of a database in simple terms, an append-only data file full of *logs*. To speed up retrieving data from a datafile we need to use an *index*. Indexes can increase the reads to our database since they help us query data faster but they slow down writes since each time we want to write to the database the index must be updated. This tradeoff is why we do not just index everything and instead those architecting/designing the system must think carefully about what to index on based on what the typical query patterns will be to maximize the speed of reads without slowing down writes too much.