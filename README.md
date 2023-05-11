# sa-neo4j

- [sa-neo4j](#sa-neo4j)
  - [Cypher CRUD](#cypher-crud)
    - [Create `Student` node and `University` node](#create-student-node-and-university-node)
    - [Read nodes](#read-nodes)
    - [Add relatioships between nodes](#add-relatioships-between-nodes)
    - [Add property](#add-property)
    - [Remove property](#remove-property)
    - [Delete relationships only](#delete-relationships-only)
    - [Delete node](#delete-node)

## Cypher CRUD

- Environment: <https://sandbox.neo4j.com/>
- Ref: <https://neo4j.com/docs/cypher-manual/current/clauses/>

### Create `Student` node and `University` node

```sql
CREATE (s:Student {name: "Kevin"}) RETURN s

CREATE (u:University {name: "MIU"}) RETURN u
```

### Read nodes

```sql
MATCH (s:Student {name: "Kevin"}) RETURN s
```

### Add relatioships between nodes

```sql
MATCH
  (s:Student),
  (u:University)
WHERE s.name = 'Kevin' AND u.name = 'MIU'
CREATE (s)-[r:GOES_TO]->(u)
RETURN type(r)
```

### Add property

```sql
MATCH (s {name: 'Kevin'})
SET s.age = 22, s.sex = 'Male'
RETURN s.name, s.age, s.sex
```

### Remove property

```sql
MATCH (s {name: 'Kevin'})
SET s.sex = null
RETURN s.name, s.age, s.sex
```

### Delete relationships only

```sql
MATCH (s:Student {name: "Kevin"})-[r:GOES_TO]->()
DELETE r
```

### Delete node

```sql
MATCH(u:University {name: "MIU"})
DELETE u
```
