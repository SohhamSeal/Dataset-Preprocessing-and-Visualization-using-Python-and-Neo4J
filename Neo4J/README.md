# How to run codes on Neo4J?

CREATE INDEX FOR (a:Author) ON (a.name);

//Create graph with undirected edges
:auto 
LOAD CSV WITH HEADERS FROM 'file:///database_for_neo4j.csv' as row
CALL{
    WITH row
    MERGE (a1: Author {name: row.`Author 1`})
    MERGE (a2: Author {name: row.`Author 2`})
    MERGE (a1)-[:WROTE_A_PAPER_WITH]-(a2)
    MERGE (a2)-[:WROTE_A_PAPER_WITH]-(a1)
} IN TRANSACTIONS of 500 ROWS

MATCH (n:Author) RETURN n LIMIT 300