-- Exercício 01

1. Adicione outro Peixe e um Hamster com nome Frodo

db.pets.insert({name: "Frodo", species: "Peixe"})
db.pets.insert({name: "Frodo", species: "Hamster"})

2. Faça uma contagem dos pets na coleção

db.pets.find().count()

3. Retorne apenas um elemento o método prático possível

db.pets.findOne()

4. Identifique o ID para o Gato Kilha.

db.pets.find({"name": "Kilha", "species": "Gato"}, {"id_":1})

5. Faça uma busca pelo ID e traga o Hamster Mike

db.pets.find({"_id": ObjectId("5eaafaca7f990bcf7dfbe236")})

6. Use o find para trazer todos os Hamsters

db.pets.find({"species": "Hamster"})

7. Use o find para listar todos os pets com nome Mike

db.pets.find({"name": "Mike"})

8. Liste apenas o documento que é um Cachorro chamado Mike

db.pets.find({"name": "Mike", "species": "Cachorro"})

