-- Exercício 01 - Aquecendo com os pets

	1. Adicione outro Peixe e um Hamster com nome Frodo

> db.pets.insert({name: "Frodo", species: "Peixe"})
> db.pets.insert({name: "Frodo", species: "Hamster"})

	2. Faça uma contagem dos pets na coleção

> db.pets.find().count()

	3. Retorne apenas um elemento o método prático possível

> db.pets.findOne()

	4. Identifique o ID para o Gato Kilha.

> db.pets.find({"name": "Kilha", "species": "Gato"}, {"id_":1})

	5. Faça uma busca pelo ID e traga o Hamster Mike

> db.pets.find({"_id": ObjectId("5eaafaca7f990bcf7dfbe236")})

	6. Use o find para trazer todos os Hamsters

> db.pets.find({"species": "Hamster"})

	7. Use o find para listar todos os pets com nome Mike

> db.pets.find({"name": "Mike"})

	8. Liste apenas o documento que é um Cachorro chamado Mike

> db.pets.find({"name": "Mike", "species": "Cachorro"})



-- Exercício 02 - Mama mia!


	1. Liste/Conte todas as pessoas que tem exatamente 99 anos. Você pode usar um count para indicar a quantidade.

>db.italians.find({"age":99}).count()

0

	2. Identifique quantas pessoas são elegíveis atendimento prioritário (pessoas com mais de 65 anos)

> db.italians.find({"age":{"$gt":65}}).count()

1738

> db.italians.find({"age":{"$gte":65}}).count()

1861

	3. Identifique todos os jovens (pessoas entre 12 a 18 anos).

> db.italians.find({"age":{"$gt":12, "$lt":18}}).count()

611

> db.italians.find({"age":{"$gte":12, "$lte":18}}).count()

840

	4. Identifique quantas pessoas tem gatos, quantas tem cachorro e quantas não tem nenhum dos dois

Gatos:
> db.italians.find({"cat":{"$exists":true}}).count()

5989

Cachorros:
> db.italians.find({"dog":{"$exists":true}}).count()

3993

Nenhum dos 2:
> db.italians.find({"$and" : [{"cat":{"$exists":false}}, {"dog":{"$exists":false}}]}).count()

2360

	5. Liste/Conte todas as pessoas acima de 60 anos que tenham gato 

> db.italians.find({"$and" : [{"age":{"$gt":65}}, {"cat":{"$exists":true}}]}).count()

1014

	6. Liste/Conte todos os jovens com cachorro

> db.italians.find({"$and" : [{"age":{"$lt":18}}, {"dog":{"$exists":true}}]}).count()

895

	7. Utilizando o $where, liste todas as pessoas que tem gato e cachorro



	8. Liste todas as pessoas mais novas que seus respectivos gatos.



	9. Liste as pessoas que tem o mesmo nome que seu bichano (gatou ou cachorro)

> db.italians.find({"$and" : [{"cat":{"$exists":true}}, {"dog":{"$exists":true}}, {$where:"this.firstname == this.cat.name"}]}).count()

39

> db.italians.find({"$and" : [{"cat":{"$exists":true}}, {"dog":{"$exists":true}}, {$where:"this.firstname == this.dog.name"}]}).count()

20

	10. Projete apenas o nome e sobrenome das pessoas com tipo de sangue de fator RH negativo

> db.italians.find({"bloodType": /-/i}).count()

4982
> db.italians.find({"bloodType": /-/i}, {"_id":0, "firstname":1, "surname":1})
{ "firstname" : "Marta", "surname" : "Pellegrini" }
{ "firstname" : "Elisabetta", "surname" : "Villa" }
{ "firstname" : "Sergio", "surname" : "Sartori" }
Type "it" for more
>

	11. Projete apenas os animais dos italianos. Devem ser listados os animais com nome e idade. Não mostre o identificado do mongo (ObjectId)

> db.italians.find({"$or" : [{"cat":{"$exists":true}}, {"dog":{"$exists":true}}]}, {"_id":0, "cat.name":1, "dog.name":1, "age":1})
{ "age" : 27, "dog" : { "name" : "Sara" } }
{ "age" : 21, "cat" : { "name" : "Mirko" } }
{ "age" : 38, "cat" : { "name" : "Federico" } }
Type "it" for more

	12. Quais são as 5 pessoas mais velhas com sobrenome Rossi?

> db.italians.find({"surname":"Rossi"}, {"_id":0, "firstname":1, "surname":1, "age":1}).sort({"age":-1}).limit(5)
{ "firstname" : "Eleonora", "surname" : "Rossi", "age" : 79 }
{ "firstname" : "Riccardo", "surname" : "Rossi", "age" : 79 }
{ "firstname" : "Daniele", "surname" : "Rossi", "age" : 78 }
{ "firstname" : "Federico", "surname" : "Rossi", "age" : 77 }
{ "firstname" : "Daniele", "surname" : "Rossi", "age" : 77 }

	13. Crie um italiano que tenha um leão como animal de estimação. Associe um nome e idade ao bichano

db.italians.insert ({"firstname" : "Giuseppi", "surname" : "Geppetttoo", "username" : "userX", "age" : 87, "email" : "Giuseppi.Geppetttoo@aol.com", "bloodType" : "O+", "id_num" : "7984561230", "registerDate" : new Date(), "ticketNumber" : 8888, "jobs" : ["Pedreiro", "Soldado"], "favFruits" : ["Abacaxi", "Melão"], "movies" : [{"title": "Missao Impossível (Sem ano)", "rating" : 0.67}], "lion" : {"name": "leaon", "age": 4} })

	14. Infelizmente o Leão comeu o italiano. Remova essa pessoa usando o Id.

_id: ObjectId("5eab4ba6399b3f308026f58d")

> db.italians.remove({"_id" : ObjectId("5eab4ba6399b3f308026f58d")})
WriteResult({ "nRemoved" : 1 })


	15. Passou um ano. Atualize a idade de todos os italianos e dos bichanos em 1.

db.italians.update({}, {"$inc": {"age": 1}}, {multi: true})

db.italians.update({}, {"$inc": {"dog.age": 1}}, {multi: true})
db.italians.update({}, {"$inc": {"cat.age": 1}}, {multi: true})

	16. O Corona Vírus chegou na Itália e misteriosamente atingiu pessoas somente com gatos e de 66 anos. Remova esses italianos.

> db.italians.find({"$and" : [{"age": 66}, {"cat":{"$exists":true}}]}).count()
117
> db.italians.remove({"$and" : [{"age": 66}, {"cat":{"$exists":true}}]})
WriteResult({ "nRemoved" : 117 })
> db.italians.find({"$and" : [{"age": 66}, {"cat":{"$exists":true}}]}).count()
0


	17. Utilizando o framework agregate, liste apenas as pessoas com nomes iguais a sua respectiva mãe e que tenha gato ou cachorro.



	18. Utilizando aggregate framework, faça uma lista de nomes única de nomes. Faça isso usando apenas o primeiro nome

> db.italians.aggregate([{$group: {"_id": "$firstname"}}])

	19. Agora faça a mesma lista do item acima, considerando nome completo.

--
db.italians.aggregate([{$group: {"_id": ["$firstname", "$surname"]}}])

	20. Procure pessoas que gosta de Banana ou Maçã, tenham cachorro ou gato, mais de 20 e menos de 60 anos.



Exercício 3 - Stockbrokers



	1. Liste as ações com profit acima de 0.5 (limite a 10 o resultado)



	2. Liste as ações com perdas (limite a 10 novamente)



	3. Liste as 10 ações mais rentáveis



	4. Qual foi o setor mais rentável?



	5. Ordene as ações pelo profit e usando um cursor, liste as ações.



	6. Renomeie o campo “Profit Margin” para apenas “profit”.



	7. Agora liste apenas a empresa e seu respectivo resultado



	8. Analise as ações. É uma bola de cristal na sua mão... Quais as três ações você investiria?



	9. Liste as ações agrupadas por setor





Exercício 3 – Fraude na Enron!

	1. Liste as pessoas que enviaram e-mails (de forma distinta, ou seja, sem
repetir). Quantas pessoas são?



	2. Contabilize quantos e-mails tem a palavra “fraud”


