Exercício 1- Retrieving Nodes
Coloque os comandos utilizado em cada item a seguir:

	Exercise 1.1: Retrieve all nodes from the database.

match(n) return (n)

	Exercise 1.2: Examine the data model for the graph.

call db.schema.visualization

	Exercise 1.3: Retrieve all Person nodes.

match (p:Person) return (p)

	Exercise 1.4: Retrieve all Movie nodes.

match (m:Movie) return (m)

Exercício 2 – Filtering queries using property values
Coloque os comandos utilizado em cada item a seguir:

	Exercise 2.1: Retrieve all movies that were released in a specific year.

match (m:Movie{released: 2000}) return (m)

	Exercise 2.2: View the retrieved results as a table.

PRINT

	Exercise 2.3: Query the database for all property keys.

call db.propertyKeys

	Exercise 2.4: Retrieve all Movies released in a specific year, returning their titles.

match (m:Movie {released:2000}) return (m.title)

	Exercise 2.5: Display title, released, and tagline values for every Movie node in the graph.

match (m:Movie) return m.title, m.tagline, m.released

	Exercise 2.6: Display more user-friendly headers in the table

match (m:Movie) return m.title as `Titulo`, m.tagline as `slogan`, m.released as `Ano`

Exercício 3 - Filtering queries using relationships
Coloque os comandos utilizado em cada item a seguir:

	Exercise 3.1: Display the schema of the database.

call db.schema.visualization

	Exercise 3.2: Retrieve all people who wrote the movie Speed Racer.

MATCH (p:Person)-[rel:WROTE]->(m:Movie {title: 'Speed Racer'})
return p

	Exercise 3.3: Retrieve all movies that are connected to the person, Tom Hanks.

match (m:Movie)<--(p:Person{name: 'Tom Hanks'})
return m

	Exercise 3.4: Retrieve information about the relationships Tom Hanks had with the set of movies retrieved earlier.

match (m:Movie)<-[rel]-(p:Person{name: 'Tom Hanks'})
return m.title, type(rel)

	Exercise 3.5: Retrieve information about the roles that Tom Hanks acted in.

match (m:Movie)<-[rel:ACTED_IN]-(p:Person{name: 'Tom Hanks'})
return m.title, rel.roles

