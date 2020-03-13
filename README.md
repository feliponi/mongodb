# mongodb
Mongo DB - Trabalho

**Exercício 1- Aquecendo com os pets

Insira os seguintes registros no MongoDB e em seguida responda as questões abaixo:

```
use petshop
db.pets.insert({name: "Mike", species: "Hamster"}) 
db.pets.insert({name: "Dolly", species: "Peixe"}) 
db.pets.insert({name: "Kilha", species: "Gato"}) 
db.pets.insert({name: "Mike", species: "Cachorro"}) 
db.pets.insert({name: "Sally", species: "Cachorro"}) 
db.pets.insert({name: "Chuck", species: "Gato"})
```
1. Adicione outro Peixe e um Hamster com nome Frodo
```
> db.pets.insert({name: "Frodo", species: "Peixe"})
WriteResult({ "nInserted" : 1 })
> db.pets.insert({name: "Frodo", species: "Hamster"})
WriteResult({ "nInserted" : 1 })
```
2. Faça uma contagem dos pets na coleção
```
> db.pets.count()
9
> 
```
3. Retorne apenas um elemento o método prático possível
```
> db.pets.findOne()
{
	"_id" : ObjectId("5e6bfb0c5e3fb5697b46b1e8"),
	"name" : "Mike",
	"species" : "Hamster"
}
>
```
4. Identifique o ID para o Gato Kilha.
```
> db.pets.find( { "name": "Kilha"} )
{ "_id" : ObjectId("5e6bfb145e3fb5697b46b1ea"), "name" : "Kilha", "species" : "Gato" }
> 
```
5. Faça uma busca pelo ID e traga o Hamster Mike
```
> db.pets.find()
{ "_id" : ObjectId("5e6bfb0c5e3fb5697b46b1e8"), "name" : "Mike", "species" : "Hamster" }
```

6. Use o find para trazer todos os Hamsters
```
> db.pets.find( { "species": "Hamster"} )
{ "_id" : ObjectId("5e6bfb0c5e3fb5697b46b1e8"), "name" : "Mike", "species" : "Hamster" }
{ "_id" : ObjectId("5e6bfb64e45daa98074f519b"), "name" : "Frodo", "species" : "Hamster" }
> 
````
7. Use o find para listar todos os pets com nome Mike
```
> db.pets.find( { "name": "Mike"} )
{ "_id" : ObjectId("5e6bfb0c5e3fb5697b46b1e8"), "name" : "Mike", "species" : "Hamster" }
{ "_id" : ObjectId("5e6bfb145e3fb5697b46b1eb"), "name" : "Mike", "species" : "Cachorro" }
> 
```
8. Liste apenas o documento que é um Cachorro chamado Mike
```
> db.pets.find(
... {
... "name": "Mike",
... "species": "Cachorro"
... }
... )
{ "_id" : ObjectId("5e6bfb145e3fb5697b46b1eb"), "name" : "Mike", "species" : "Cachorro" }
> 
```


**Exercício 2 – Mama mia!

Importe o arquivo dos italian-people.js do seguinte endereço: Downloads NoSQL FURB. Em seguida, importe o mesmo com o seguinte comando:
```
mongo italian-people.js
````

Analise um pouco a estrutura dos dados e em seguida responda:
1. Liste/Conte todas as pessoas que tem exatamente 99 anos. Você pode usar um count para indicar a quantidade.
2. Identifique quantas pessoas são elegíveis atendimento prioritário (pessoas com mais de 65 anos)
3. Identifique todos os jovens (pessoas entre 12 a 18 anos).
4. Identifique quantas pessoas tem gatos, quantas tem cachorro e quantas
não tem nenhum dos dois
5. Liste/Conte todas as pessoas acima de 60 anos que tenham gato
6. Liste/Conte todos os jovens com cachorro
7. Utilizando o $where, liste todas as pessoas que tem gato e cachorro
8. Liste todas as pessoas mais novas que seus respectivos gatos.
9. Liste as pessoas que tem o mesmo nome que seu bichano (gatou ou
cachorro)
10. Projete apenas o nome e sobrenome das pessoas com tipo de sangue de
fator RH negativo
11. Projete apenas os animais dos italianos. Devem ser listados os animais
com nome e idade. Não mostre o identificado do mongo (ObjectId)
12. Quais são as 5 pessoas mais velhas com sobrenome Rossi?
13. Crie um italiano que tenha um leão como animal de estimação. Associe
um nome e idade ao bichano
14. Infelizmente o Leão comeu o italiano. Remova essa pessoa usando o Id.
15. Passou um ano. Atualize a idade de todos os italianos e dos bichanos em
1.
16. O Corona Vírus chegou na Itália e misteriosamente atingiu pessoas
somente com gatos e de 66 anos. Remova esses italianos.
17. Utilizando o framework agregate, liste apenas as pessoas com nomes
iguais a sua respectiva mãe e que tenha gato ou cachorro.
18. Utilizando aggregate framework, faça uma lista de nomes única de
nomes. Faça isso usando apenas o primeiro nome
19. Agora faça a mesma lista do item acima, considerando nome completo.
20. Procure pessoas que gosta de Banana ou Maçã, tenham cachorro ou gato,
mais de 20 e menos de 60 anos.


**Exercício 3 - Stockbrokers

Bancos NoSQL – FURB

Importe o arquivo stocks.json do repositório Downloads NoSQL FURB. Esses dados são dados reais da bolsa americana de 2015. A importação do arquivo JSON é um pouco diferente da execução de um script:

Analise um pouco a estrutura dos dados novamente e em seguida, responda as seguintes perguntas:
1. Liste as ações com profit acima de 0.5 (limite a 10 o resultado)
2. Liste as ações com perdas (limite a 10 novamente)
3. Liste as 10 ações mais rentáveis
4. Qual foi o setor mais rentável?
5. Ordene as ações pelo profit e usando um cursor, liste as ações.
6. Renomeie o campo “Profit Margin” para apenas “profit”.
7. Agora liste apenas a empresa e seu respectivo resultado
8. Analise as ações. É uma bola de cristal na sua mão... Quais as três ações
você investiria?
9. Liste as ações agrupadas por setor
 ```
 mongoimport --db stocks --collection stocks --file
 stocks.json
 ```
