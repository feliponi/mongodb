# mongodb
Mongo DB - Trabalho

## Exercício 1- Aquecendo com os pets

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


## Exercício 2 – Mama mia!

Importe o arquivo dos italian-people.js do seguinte endereço: Downloads NoSQL FURB. Em seguida, importe o mesmo com o seguinte comando:
```
mongo italian-people.js
````

Analise um pouco a estrutura dos dados e em seguida responda:

1. Liste/Conte todas as pessoas que tem exatamente 99 anos. Você pode usar um count para indicar a quantidade.
```
> db.italians.find( {"age": 99} ).count()
0
> 
```

2. Identifique quantas pessoas são elegíveis atendimento prioritário (pessoas com mais de 65 anos)
```
> db.italians.find( { age : { $gte: 65 } } ).count()
1913
> 
```
3. Identifique todos os jovens (pessoas entre 12 a 18 anos).
```
> db.italians.find( { age : { $in: [12, 18] } } ).count()
258
> 
```
4. Identifique quantas pessoas tem gatos, quantas tem cachorro e quantas
não tem nenhum dos dois

gatos

```
> db.italians.aggregate(
... [
... {"$group" : {_id: "$cat", count:{$sum:1}}}
... ]
... )
{ "_id" : { "name" : "Mirko", "age" : 1 }, "count" : 4 }
{ "_id" : { "name" : "Anna", "age" : 11 }, "count" : 8 }
{ "_id" : { "name" : "Vincenzo", "age" : 14 }, "count" : 3 }
{ "_id" : { "name" : "Eleonora", "age" : 8 }, "count" : 4 }
{ "_id" : { "name" : "Federico", "age" : 2 }, "count" : 5 }
{ "_id" : { "name" : "Michele", "age" : 0 }, "count" : 5 }
{ "_id" : { "name" : "Michele", "age" : 15 }, "count" : 2 }
{ "_id" : { "name" : "Luigi", "age" : 10 }, "count" : 5 }
{ "_id" : { "name" : "Simona", "age" : 16 }, "count" : 6 }
{ "_id" : { "name" : "Paolo", "age" : 15 }, "count" : 4 }
{ "_id" : { "name" : "Roberto", "age" : 17 }, "count" : 7 }
{ "_id" : { "name" : "Veronica", "age" : 16 }, "count" : 3 }
{ "_id" : { "name" : "Claudio", "age" : 17 }, "count" : 1 }
{ "_id" : { "name" : "Antonella", "age" : 0 }, "count" : 3 }
{ "_id" : { "name" : "Anna", "age" : 16 }, "count" : 2 }
{ "_id" : { "name" : "Laura", "age" : 6 }, "count" : 3 }
{ "_id" : { "name" : "Fabrizio", "age" : 2 }, "count" : 1 }
{ "_id" : { "name" : "Giuseppe", "age" : 7 }, "count" : 1 }
{ "_id" : { "name" : "Paola", "age" : 4 }, "count" : 6 }
{ "_id" : { "name" : "Maria", "age" : 1 }, "count" : 3 }
Type "it" for more
> 
```
cachorros

```
db.italians.aggregate( [ {"$group" : {_id: "$dog", count:{$sum:1}}} ] )
{ "_id" : { "name" : "Alex", "age" : 10 }, "count" : 3 }
{ "_id" : { "name" : "Emanuele", "age" : 3 }, "count" : 4 }
{ "_id" : { "name" : "Ilaria", "age" : 3 }, "count" : 2 }
{ "_id" : { "name" : "Cinzia", "age" : 1 }, "count" : 2 }
{ "_id" : { "name" : "Angelo", "age" : 8 }, "count" : 2 }
{ "_id" : { "name" : "Massimo", "age" : 6 }, "count" : 5 }
{ "_id" : { "name" : "Antonio", "age" : 4 }, "count" : 3 }
{ "_id" : { "name" : "Elisabetta", "age" : 9 }, "count" : 3 }
{ "_id" : { "name" : "Maurizio", "age" : 5 }, "count" : 4 }
{ "_id" : { "name" : "Silvia", "age" : 16 }, "count" : 3 }
{ "_id" : { "name" : "Roberta", "age" : 14 }, "count" : 3 }
{ "_id" : { "name" : "Simona", "age" : 15 }, "count" : 3 }
{ "_id" : { "name" : "Marco", "age" : 15 }, "count" : 1 }
{ "_id" : { "name" : "Anna", "age" : 5 }, "count" : 5 }
{ "_id" : { "name" : "Roberta", "age" : 15 }, "count" : 2 }
{ "_id" : { "name" : "Stefania", "age" : 7 }, "count" : 5 }
{ "_id" : { "name" : "Nicola", "age" : 12 }, "count" : 2 }
{ "_id" : { "name" : "Nicola", "age" : 4 }, "count" : 2 }
{ "_id" : { "name" : "Valeira", "age" : 4 }, "count" : 6 }
{ "_id" : { "name" : "Sara", "age" : 5 }, "count" : 1 }
```
``` 
db.italians.aggregate( [ {"$group" : {_id: {dog:"$dog",cat:"$cat"}, count:{$sum:-1}}} ] )
```
5. Liste/Conte todas as pessoas acima de 60 anos que tenham gato
```
db.italians.aggregate( [ { $match: { age: { $gte: 60 } } }, {"$group" : {_id: "$cat", count:{$sum:1}} } ] )
{ "_id" : { "name" : "Valeira", "age" : 1 }, "count" : 1 }
{ "_id" : { "name" : "Ilaria", "age" : 12 }, "count" : 3 }
{ "_id" : { "name" : "Giusy", "age" : 1 }, "count" : 1 }
{ "_id" : { "name" : "Giorgio", "age" : 13 }, "count" : 3 }
```

6. Liste/Conte todos os jovens com cachorro
```
db.italians.aggregate( [ { $match: { age: { $lte: 60 } } }, {"$group" : {_id: "$dog", count:{$sum:1}} } ] )
{ "_id" : { "name" : "Alex", "age" : 10 }, "count" : 3 }
{ "_id" : { "name" : "Emanuele", "age" : 3 }, "count" : 1 }
{ "_id" : { "name" : "Ilaria", "age" : 3 }, "count" : 2 }

```

7. Utilizando o $where, liste todas as pessoas que tem gato e cachorro
```
 db.italians.find( { cat: { $exists: false, $not: {$size: 0} } }).count()
3992
```

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


## Exercício 3 - Stockbrokers

Bancos NoSQL – FURB

Importe o arquivo stocks.json do repositório Downloads NoSQL FURB. Esses dados são dados reais da bolsa americana de 2015. A importação do arquivo JSON é um pouco diferente da execução de um script:

Analise um pouco a estrutura dos dados novamente e em seguida, responda as seguintes perguntas:
1. Liste as ações com profit acima de 0.5 (limite a 10 o resultado)
```
db.stocks.find( { "Profit Margin" : { $gte: 0.5 } } ).limit(10)
{ "_id" : ObjectId("52853800bb1177ca391c180f"), "Ticker" : "AB", "Profit Margin" : 0.896, "Institutional Ownership" : 0.368, "EPS growth past 5 years" : -0.348, "Total Debt/Equity" : 0, "Return on Assets" : 0.086, "Sector" : "Financial", "P/S" : 13.25, "Change from Open" : 0.0047, "Performance (YTD)" : 0.3227, "Performance (Week)" : -0.0302, "Insider Transactions" : 0.5973, "P/B" : 1.4, "EPS growth quarter over quarter" : 2.391, "Payout Ratio" : 1.75, "Performance (Quarter)" : 0.0929, "Forward P/E" : 12.58, "P/E" : 15.82, "200-Day Simple Moving Average" : 0.0159, "Shares Outstanding" : 92.26, "Earnings Date" : ISODate("2013-10-24T12:30:00Z"), "52-Week High" : -0.1859, "Change" : -0.0009, "Analyst Recom" : 3, "Volatility (Week)" : 0.0264, "Country" : "USA", "Return on Equity" : 0.087, "50-Day Low" : 0.123, "Price" : 21.5, "50-Day High" : -0.0574, "Return on Investment" : 0.033, "Shares Float" : 86.66, "Dividend Yield" : 0.0743, "EPS growth next 5 years" : 0.08,
```
2. Liste as ações com perdas (limite a 10 novamente)
```
db.stocks.find( { "Profit Margin" : { $lte: 0 } } ).limit(10)
{ "_id" : ObjectId("52853800bb1177ca391c1806"), "Ticker" : "AAOI", "Profit Margin" : -0.023, "Institutional Ownership" : 0.114, "EPS growth past 5 years" : 0, "Current Ratio" : 1.5, "Return on Assets" : -0.048, "Sector" : "Technology", "P/S" : 2.3, "Change from Open" : -0.0215, "Performance (YTD)" : 0.2671, "Performance (Week)" : -0.0381, "Quick Ratio" : 0.9, "EPS growth quarter over quarter" : -1, "Forward P/E" : 12.77, "200-Day Simple Moving Average" : 0.0654, "Shares Outstanding" : 12.6, "52-Week High" : -0.0904, "P/Cash" : 16.23, "Change" : -0.0269, "Analyst Recom" : 1.8, "Volatility (Week)" : 0.0377, "Country" : "USA", "Return on Equity" : 0.043, "50-Day Low" : 0.3539, "Price" : 12.28, "50-Day High" : -0.0904, "Return on Investment" : -0.004, "Shares Float" : 11.46, "Industry" : "Semiconductor - Integrated Circuits", "Sales growth quarter over quarter" : 0.256, "Operating Margin" : -0.007, "EPS (ttm)" : -0.13, "Float Short" : 0.0011, "52-Week Low" : 0.3539, "Average True Range" : 0.63, "EPS growth next year" : 38.52, "Company" : "Applied Optoelectronics, Inc.", "Gap" : -0.0055, "Relative Volume" : 0.12, "Volatility (Month)" : 0.0608, "Market Cap" : 159.06, "Volume" : 12203, "Gross Margin" : 0.292, "Short Ratio" : 0.12, "Insider Ownership" : 0.021, "20-Day Simple Moving Average" : -0.0251, "Performance (Month)" : 0.2397, "Average Volume" : 110.95, "EPS growth this year" : 0.833, "50-Day Simple Moving Average" : 0.0654 }

```

3. Liste as 10 ações mais rentáveis
```
 db.stocks.find()._addSpecial( "$orderby", {"Profit Margin" : -1 } ).limit(10)
{ "_id" : ObjectId("52853800bb1177ca391c17ff"), "Ticker" : "A", "Profit Margin" : 0.137, "Institutional Ownership" : 0.847, "EPS growth past 5 years" : 0.158, "Total Debt/Equity" : 0.56, "Current Ratio" : 3, "Return on Assets" : 0.089, "Sector" : "Healthcare", "P/S" : 2.54, "Change from Open" : -0.0148, "Performance (YTD)" : 0.2605, "Performance (Week)" : 0.0031, "Quick Ratio" : 2.3, "Insider Transactions" : -0.1352, "P/B" : 3.63, "EPS growth quarter over quarter" : -0.29, "Payout Ratio" : 0.162, "Performance (Quarter)" : 0.0928, "Forward P/E" : 16.11, "P/E" : 19.1, "200-Day Simple Moving Average" : 0.1062, "Shares Outstanding" : 339, "Earnings Date" : ISODate("2013-11-14T21:30:00Z"), "52-Week High" : -0.0544, "P/Cash" : 7.45, "Change" : -0.0148, "Analyst Recom" : 1.6, "Volatility (Week)" : 0.0177, "Country" : "USA", "Return on Equity" : 0.182, "50-Day Low" : 0.0728, "Price" : 50.44, "50-Day High" : -0.0544, "Return on Investment" : 0.163, "Shares Float" : 330.21, "Dividend Yield" : 0.0094, "EPS growth next 5 years" : 0.0843, "Industry" : "Medical Laboratories & Research", "Beta" : 1.5, "Sales growth quarter over quarter" : -0.041, "Operating Margin" : 0.187, "EPS (ttm)" : 2.68, "PEG" : 2.27, "Float Short" : 0.008, "52-Week Low" : 0.4378, "Average True Range" : 0.86, "EPS growth next year" : 0.1194, "Sales growth past 5 years" : 0.048, "Company" : "Agilent Technologies Inc.", "Gap" : 0, "Relative Volume" : 0.79, "Volatility (Month)" : 0.0168, "Market Cap" : 17356.8, "Volume" : 1847978, "Gross Margin" : 0.512, "Short Ratio" : 1.03, "Performance (Half Year)" : 0.1439, "Relative Strength Index (14)" : 46.51, "Insider Ownership" : 0.001, "20-Day Simple Moving Average" : -0.0172, "Performance (Month)" : 0.0063, "P/Free Cash Flow" : 19.63, "Institutional Transactions" : -0.0074, "Performance (Year)" : 0.4242, "LT Debt/Equity" : 0.56, "Average Volume" : 2569.36, "EPS growth this year" : 0.147, "50-Day Simple Moving Average" : -0.0055 }
{ "_id" : ObjectId("52853800bb1177ca391c1801"), "Ticker" : "AADR", "Sector" : "Financial", "Change from Open" : 0.0055, "Performance (YTD)" : 0.1809, "Performance (Week)" : -0.0134, "Performance (Quarter)" : 0.061, "200-Day Simple Moving Average" : 0.0693, "52-Week High" : -0.0194, "Change" : 0.0064, "Volatility (Week)" : 0.0072, "Country" : "USA", "50-Day Low" : 0.0792, "Price" : 36.4, "50-Day High" : -0.0194, "Dividend Yield" : 0.005, "Industry" : "Exchange Traded Fund", "52-Week Low" : 0.2727, "Average True Range" : 0.31, "Company" : "WCM/BNY Mellon Focused Growth ADR ETF", "Gap" : 0.0008, "Relative Volume" : 0.72, "Volatility (Month)" : 0.0052, "Volume" : 6660, "Performance (Half Year)" : 0.04, "Relative Strength Index (14)" : 51.91, "20-Day Simple Moving Average" : -0.0054, "Performance (Month)" : 0.0183, "Performance (Year)" : 0.229, "Average Volume" : 10.07, "50-Day Simple Moving Average" : 0.0158 }
```

4. Qual foi o setor mais rentável?


5. Ordene as ações pelo profit e usando um cursor, liste as ações.
```
$cursor = db.stocks.find()._addSpecial( "$orderby", {"Profit Margin" : 1 } )
```

6. Renomeie o campo “Profit Margin” para apenas “profit”.
```
db.stocks.updateMany( {}, { $rename: {"Profit Margin" : "profit" } } )
{ "acknowledged" : true, "matchedCount" : 6756, "modifiedCount" : 4302 }
```

7. Agora liste apenas a empresa e seu respectivo resultado
```
$cursor = db.stocks.aggregate({ $project : { Ticker : 1, profit : 1 } } )
{ "_id" : ObjectId("52853800bb1177ca391c17ff"), "Ticker" : "A", "profit" : 0.137 }
{ "_id" : ObjectId("52853800bb1177ca391c1801"), "Ticker" : "AADR" }
{ "_id" : ObjectId("52853800bb1177ca391c1802"), "Ticker" : "AAIT" }
{ "_id" : ObjectId("52853800bb1177ca391c1800"), "Ticker" : "AA", "profit" : 0.013 }
{ "_id" : ObjectId("52853800bb1177ca391c1804"), "Ticker" : "AAME", "profit" : 0.056 }
{ "_id" : ObjectId("52853800bb1177ca391c1805"), "Ticker" : "AAN", "profit" : 0.06 }
{ "_id" : ObjectId("52853800bb1177ca391c1806"), "Ticker" : "AAOI", "profit" : -0.023 }
{ "_id" : ObjectId("52853800bb1177ca391c1807"), "Ticker" : "AAON", "profit" : 0.105 }
{ "_id" : ObjectId("52853800bb1177ca391c1803"), "Ticker" : "AAMC" }
{ "_id" : ObjectId("52853800bb1177ca391c1809"), "Ticker" : "AAPL", "profit" : 0.217 }
{ "_id" : ObjectId("52853800bb1177ca391c1808"), "Ticker" : "AAP", "profit" : 0.063 }
{ "_id" : ObjectId("52853800bb1177ca391c180a"), "Ticker" : "AAT", "profit" : 0.155 }
{ "_id" : ObjectId("52853800bb1177ca391c180b"), "Ticker" : "AAU" }
{ "_id" : ObjectId("52853800bb1177ca391c180c"), "Ticker" : "AAV", "profit" : -0.232 }
{ "_id" : ObjectId("52853800bb1177ca391c180e"), "Ticker" : "AAXJ" }
{ "_id" : ObjectId("52853800bb1177ca391c180f"), "Ticker" : "AB", "profit" : 0.896 }
{ "_id" : ObjectId("52853800bb1177ca391c1810"), "Ticker" : "ABAX", "profit" : 0.1 }
{ "_id" : ObjectId("52853800bb1177ca391c1811"), "Ticker" : "ABB", "profit" : 0.069 }
{ "_id" : ObjectId("52853800bb1177ca391c180d"), "Ticker" : "AAWW", "profit" : 0.071 }
{ "_id" : ObjectId("52853800bb1177ca391c1812"), "Ticker" : "ABBV", "profit" : 0.24 }
```
8. Analise as ações. É uma bola de cristal na sua mão... Quais as três ações
você investiria?
ABB, ABAX e ABBV

9. Liste as ações agrupadas por setor
 ```
 mongoimport --db stocks --collection stocks --file
 stocks.json
 ```
