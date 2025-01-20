
# Neo4j (Graph Database) Quick Learning

<img width="1007" alt="image" src="https://github.com/user-attachments/assets/83ce7bc7-1985-4cdc-b92f-a37ef01752c6" />

---

## 1. What is Neo4j?
- Neo4j is a native graph database that uses **nodes** and **relationships** to represent and store data.
- It is ideal for connected data scenarios such as social networks, recommendation engines, fraud detection, and knowledge graphs.

---

## 2. Core Concepts
### Nodes
- Represent entities or objects (e.g., `Person`, `Product`).
- Visualized as circles in the graph.

### Relationships
- Represent connections between nodes (e.g., `FRIENDS_WITH`, `BOUGHT`).
- Directed and labeled; can include properties.

### Properties
- Key-value pairs associated with nodes and relationships.

### Labels
- Categories assigned to nodes (e.g., `User`).

### Cypher Query Language (CQL)
- SQL-like language used to query graph data.
- Example: `MATCH (n:Person {name: 'Alice'}) RETURN n`.

---

## 3. Installing and Setting Up Neo4j
1. **Download:** [Neo4j Download Page](https://neo4j.com/download/)
2. **Run:** Use Neo4j Desktop, Neo4j Aura (Cloud), or Neo4j Sandbox (Free).

---

## 4. Cypher Query Language Basics

### MATCH
Retrieve data.
```cypher
MATCH (p:Person {name: 'Alice'}) RETURN p
```

### CREATE
Add nodes and relationships.
```cypher
CREATE (p:Person {name: 'Alice', age: 30})
CREATE (p)-[:FRIENDS_WITH]->(q:Person {name: 'Bob'})
```

### MERGE
Create if not exists; match if it does.
```cypher
MERGE (p:Person {name: 'Charlie'})
```

### UPDATE
Update node/relationship properties.
```cypher
MATCH (p:Person {name: 'Alice'})
SET p.age = 31
```

### DELETE
Remove nodes or relationships.
```cypher
MATCH (p:Person {name: 'Alice'})
DELETE p
```

### RETURN
Fetch results.
```cypher
MATCH (p:Person)
RETURN p.name, p.age
```

### Detach 
In Neo4j, a DETACH DELETE query is used to delete a node and all its connected relationships in one operation. This is especially useful when a node has relationships that would otherwise cause a constraint violation if you attempted to delete the node directly.

```cypher
MATCH (n:Label {property: value})
DETACH DELETE n
```

### Relationships
Query relationships between nodes.
```cypher
MATCH (a:Person)-[r:FRIENDS_WITH]->(b:Person)
RETURN a.name, b.name
```

---

## 5. Indexing and Constraints

### Indexing
Improves query performance.
```cypher
CREATE INDEX FOR (p:Person) ON (p.name)
```

### Constraints
Enforces data integrity.
```cypher
CREATE CONSTRAINT ON (p:Person) ASSERT p.name IS UNIQUE
```

---

## 6. Common Use Cases

### Social Network Analysis
Find mutual friends.
```cypher
MATCH (a:Person)-[:FRIENDS_WITH]-(b:Person)-[:FRIENDS_WITH]-(c:Person)
WHERE a.name = 'Alice' AND c.name <> 'Alice'
RETURN c.name
```
> **Note:** Added detailed breakdown as it was difficult to understand what's happening initially.

1. **`(a:Person)`**: Matches a node with the label `Person`. This node represents the person named Alice.
2. **`[:FRIENDS_WITH]`**: Matches relationships labeled `FRIENDS_WITH`. These are the connections between friends.
3. **`(b:Person)`**: Represents friends of Alice.
4. **`[:FRIENDS_WITH]-(c:Person)`**: Finds other friends (`c`) of Alice's friends (`b`).



### Recommendation Systems
Recommend items based on user behavior.
```cypher
MATCH (u:User)-[:BOUGHT]->(p:Product)<-[:BOUGHT]-(other:User)
WHERE u.name = 'Alice'
RETURN DISTINCT p.name
```

### Fraud Detection
Detect suspicious transaction patterns.
```cypher
MATCH (a:Account)-[t:TRANSFER]->(b:Account)
WHERE t.amount > 10000
RETURN a, b, t
```

---

## 7. Advanced Features

### Graph Algorithms
- Includes algorithms like PageRank, Shortest Path, and Community Detection.

### APOC Procedures
- Utility library for advanced graph operations.
```cypher
CALL apoc.help('text')
```

### Spatial and Temporal Queries
- Query geo-spatial and time-based data effectively.


---


### Use Case Knowledge
  - Social network analysis.
  - Recommendation systems.

---

## Resources
- [Official Documentation](https://neo4j.com/docs/)
- [Cypher Reference Card](https://neo4j.com/docs/cypher-refcard/current/)
- [Neo4j GraphAcademy](https://neo4j.com/graphacademy/)

---

### Reference 

- [Springboot neo4j integration](https://www.youtube.com/watch?v=LjtcrWkC0-E)
- [End to end on Graph DB - neo4K](https://www.youtube.com/watch?v=_IgbB24scLI)
- [Neo4j 1 hour version](https://www.youtube.com/watch?v=8jNPelugC2s&t=64s)
- [Springboot Neo4K](https://www.youtube.com/watch?v=GerN3MGm9Js)
- [Google - Understanding graph databases with Neo4j](https://www.youtube.com/watch?v=gojEIojo7-I&t=71s)
- [why Graph Databases is so Fast](https://www.youtube.com/watch?v=Sdw_D-Gllac)
- [java techie springboot neo4j integration](https://www.youtube.com/watch?v=RjEK3Q6GMzw)
