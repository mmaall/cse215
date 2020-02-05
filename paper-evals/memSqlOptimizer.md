---
documentclass: article
fontsize: 12pt
mainfont: Roboto
geometry: [top=3cm, bottom=3cm, left=3cm, right=3cm]
---

# Paper Evaluation
# The MemSQL Query Optimizer: A modern optimizer for real-time analytics in a distributed database 
#### Michael Lanthier

The MemSQL Optimizer re-implemented how database do query optimization on a distributed scale. By braking query optimization into separate pieces that are aware of the way data is distributed across nodes, MemSQL is better able to optimize and cache query plans for real time processing of data. MemSQL uses a rewriter to decide whether a query should be rewritten based off of the cost of a distributed query. It then runs it through a enumerator which determines how data will be joined together because of the distributed nature of the database. It will then use the planner to convert the logical execution plan into smaller distributed queries and data movement operations. 

## Questions/Comments

1. Are network speeds part of the heuristics? If one node consistently takes longer to reply with data will the system adapt and come up with plans that work around that slow node? If network speed between nodes is extremely variable then that could impact which query plan is best. 

2. Breaking down standard industry benchmarks to show how their system differs from traditional systems was a very effective technique in showing how MemSQL operates differently as well as what makes it work better. 

3. Could running the aggregators on the same systems as leaf nodes reduce time? If the network is not very fast and aggregators and leaf nodes are on different systems, at a minimum all the data that is being outputted by the query must be sent to the aggregator. If aggregators operated on leaf nodes, an aggregator that got a query could come up with a query plan and either do it itself and maybe some of the data is already on itself or it could forward it to another aggregator to run the query which may reduce the amount of data that later needs to be streamed across the network. 
