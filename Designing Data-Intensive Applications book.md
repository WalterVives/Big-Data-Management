## Designing Data-Intensive Applications.

## Chapter 2
### Data Models and Query Languages

1. **What is the goal of the relational model?**  
It was to hide that implementation datail behind a cleaner interface.

2. **What are some of the driving forces behind the adoption of NoSQL databases?**

A need for greater scalability than relational databases can easily achieve, including very large datasets or very high write throughput.  

A widespread preference for free and open source software over commercial database products.  

Specialized query operations that are not well supported by the relational model.  

Frustration with the restrictiveness of relational schemas, and a desire for a more
dynamic and expressive data model.

3. **what is the CODASYL model and what allow us?**

The CODASYL model was a generalization of the hierarchical model. In the tree structure of the hierarchical model, every record has exactly one parent; in the network model, a record could have multiple parents.

This allowed many-to-one and many-to-many relationships to be modeled.

4. **What are the strengths in favor of the relational database against the document databases? and vice versa**

The document data model are schema flexibility, better performance due to locality, and that for some applications it is closer to the data structures used by the application.
The relational model provide better support for joins, and many-to-one and many-to-many relationships.
