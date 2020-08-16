# NoSQL подход к работе с большими данными
## Практика работы с MongoDB через инструмент mongo shell

1. Открыть online терминал по ссылке: https://docs.mongodb.com/manual/tutorial/getting-started/

2. Создать базу данных:
```
use products
```
3. Вставить 4 документа по товарам. Атрибуты:
* название
* категория (2 товара с одной категории, 2 товара из другой)
* цена
* количество товаров на складе
```
db.product.insertMany([
{product:'potatoes',category:'vegetable',price:30,amount:1000},
{product:'onion',category:'vegetable',price:20,amount:500},
{product:'apple',category:'fruit',price:40,amount:700},
{product:'pear',category:'fruit',price:50,amount:600}
])
```
4. Рассчитать остаточную стоимость товаров в каждой категории (сумма цены, умноженной на остаток):
```
db.product.aggregate(
   [
     { $project: {  category: 1, total: { $multiply: [ "$price", "$amount" ] } } },
     {$group:{ _id:'$category', cost:{$sum:'$total'}}}
   ]
)
```
5. Уменьшить количество товара на 1:
```
db.product.updateOne({product:'apple'},{$inc:{amount:-1}})
```
6. Вывести top-2 самых дорогих товара:
```
db.product.find({product}).sort({price: -1}).limit(2)
```
<details>
  <summary>Скрины заданий</summary>

![п1-3](https://github.com/leonnika/big_data-mongoDB/blob/master/scrin.PNG) 

</details>