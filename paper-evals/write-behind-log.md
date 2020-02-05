---
documentclass: article
fontsize: 12pt
mainfont: Roboto
geometry: [top=3cm, bottom=3cm, left=3cm, right=3cm]
---

# Paper Evaluation: Write Behind Logging
#### Michael Lanthier
Write behind logging is a new logging technique used to exploit the durability and fine grained writes provided by non-volatile memory (NVM) in systems using NVM as durrable storage. This technique writes tuples directly to durable storage when changes are made in the database and then writes the redo information to the logs. It is also able to reduce recovery time by removing checkpointing and a single parse of the logs allows for the removal of the redo and undo phases. These changes reduce the storage needs as well as decrease recovery time.  


## Questions/Comments

1. I feel like I'm missing something key but if NVM is considered durrable storage why do we need a log? Can't we just stage the changes of a transaction and then write them fully when the commit is received? 

2. Does the dirty tuple table ever take up a substantial amount of storage? If you are making huge batch updates or inserts the db would be keeping track of alot of tuples.

3. Could a system similar to this be designed using NVM and disk? The system would act as usual with a WBL but had the data replicated to disk asynchronously. Only when the buffer pool held in NVM is full would a flush to disk be required. Is this feasable or am I missing something completely? This may be a way to balance the cheap affodability of disk and the fast but more expensive persistant NVM.  
