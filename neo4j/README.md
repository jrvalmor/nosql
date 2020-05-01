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


Exercício 4 – Filtering queries using WHERE clause
Coloque os comandos utilizado em cada item a seguir:

	Exercise 4.1: Retrieve all movies that Tom Cruise acted in.

match (m:Movie) <-[rel:ACTED_IN]-(p:Person)
where p.name = 'Tom Cruise'

return m.title

	Exercise 4.2: Retrieve all people that were born in the 70’s.

match (p:Person) where p.born = 1970 
return p

	Exercise 4.3: Retrieve the actors who acted in the movie The Matrix who were born after 1960.

match (m:Movie) <-[rel:ACTED_IN]-(p:Person)
where m.title = 'The Matrix' and p.born > 1960

return p.name

	Exercise 4.4: Retrieve all movies by testing the node label and a property.

match (m:Movie)
where m.title = 'The Matrix'
return m.title

	Exercise 4.5: Retrieve all people that wrote movies by testing the relationship between two nodes.

match (x)-[rel]->(y)
where x:Person and type(rel) = 'WROTE' and y:Movie
return x.name, type(rel), y.title

	Exercise 4.6: Retrieve all people in the graph that do not have a property.

match (m:Movie) where not exists(m.rating)
return m

	Exercise 4.7: Retrieve all people related to movies where the relationship has a property.

match (p:Person)-[rel]->(m:Movie)
where exists(rel.summary)
return p

	Exercise 4.8: Retrieve all actors whose name begins with James.

match (p:Person) -[:ACTED_IN]-> (m:Movie)
where p.name =~'James.*'
return p.name

	Exercise 4.9: Retrieve all all REVIEW relationships from the graph with filtered results.

match (p:Person) -[rel:REVIEWED]-> (m:Movie)
where rel.summary CONTAINS 'movie'
return m.title, rel.summary

	Exercise 4.10: Retrieve all people who have produced a movie, but have not directed a movie.

match (p:Person) -[rel:PRODUCED]-> (m:Movie)
where not (p)-[:DIRECTED]-> (m)
return p.name

	Exercise 4.11: Retrieve the movies and their actors where one of the actors also directed the movie.

match (p:Person) -[rel:ACTED_IN]->(m:Movie)
where exists ((p)-[:DIRECTED]-> (m))
return m.name

	Exercise 4.12: Retrieve all movies that were released in a set of years.

match (m:Movie) 
where m.released in [2000, 2001, 2003]
return m.title


	Exercise 4.13: Retrieve the movies that have an actor’s role that is the name of the movie.

match (p:Person)-[rel:ACTED_IN]->(m:Movie)
where m.title = rel.roles
return m.title
