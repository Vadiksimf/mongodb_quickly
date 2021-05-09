# mongodb_quickly

MongoDB - uses BSON data format (typed JSON) </br>
MongoDB - NoSQL DB >
```
DB > Collections > Documents 
     Users/Posts | user/post
```

## Установка MongoDB
1. Установка Mongodb Community Server / Compass Community
2. С://data/db - создание базы данных
3. В папке mongodb - mongod.exe - запуск сервера
4. В папке mongodb - mongo.exe  - запуск shell --> войти в дирректорию спрограммой --> .\mongo.exe
5. Создание быстрого вызова из PowerShell
Свойства системы -> Дополнительно -> Переменные среды -> path (создать путь к папке C:\Program Files\MongoDB\Server\4.2\bin) - получаем доступ к запуску mongo.exe из любой дирректории в PowerShell </br>
mongod.exe - запуск mongodb </br>
mongo.exe  - открытие mongoshell

### -------------- Базовые команды--------------------------------------
use notours-test | создание новой / подключение к существующей базе данных
db               | получение базы данных
show dbs         | показать базы данных
show collections | показать имя коллекции текущей базы данных
quit()           | выход

## ----------------CRUD operations--------------------------------------
### ---------------Создание данных--------------------------------------

db           |  .tours   |  .insertOne()
-------------|-----------|----------------
текущая база | коллекция | команда

```
db.tours.insertOne({name: "The Forest Hiker", price: 297, rating: 4.7}) 
```
Добавление данных нескольких объектов  
```
db.tours.insertMany(
    [
        {name: "The Sea Explorer", price: 497, rating:4.7}, 
        {name: "The Snow Adwenturer", price: 997, rating: 4.9, difficulty: easy}
    ]
)    
```


### ------------------Поиск данных-----------------------------------
Команда                              | Описание
-------------------------------------|---------------------------------
 db.tours.find()                     | найти всю коллекцию tours и показать
 db.tours.find({name: "The Forest Hiker"}) | поиск по параметрам
db.tours.find({price: {$lte: 500} })    | $lte - less than equal
<= $lte                                    | less than + equal
<  $lt                                     | less than
\>= $gte                                   | grater than + equal
\>  $gt                                    | grater than

Условие и (&)
```
db.tours.find({ price: {$lt: 500}, rating: {$gte: 4.7} })
```
Условие или - $or
```
db.tours.find({ $or: [{price: {$lt: 500}}, {rating: {$gte: 4.7}}] })
```
Выводимые поля - только имя = name: 1
```
db.tours.find({ $or: [...] }, {name: 1})
```

### ------------------Обновление данных ----------------------------------
Обновляет один или первый найденный документ
```
db.tours.updateOne({name: "The Snow Adwenturer"}, {$set: {price: 597}} )
                    поиск нужных данных/filter  | перезаписываемое/новое значение
```
```
db.tours.updateMany(
    { price: {$gte: 500}, rating: {$gte: 4.8} },  - filter
    { $set: {premium: true} }                     - set
)
```
Перемещение
```
db.tours.replaceOne()  
```

### ------------------Удаление данных -------------------------------------

Удаление первого значения меньше 4.8
```
db.tours.deleteOne({ rating: {$lt: 4.8} })
```
Удаление всех значений меньше 4.8
```
db.tours.deleteMany({ rating: {$lt: 4.8} })
```
Удаление ВСЕХ значений базы данных
```
db.tours.deleteMany({})           
```

### ------------------ Работа с интерфейсом -------------------------------
// Установить MongoDB Compas </br>
// Создание DB в Atlas </br>
// Доступ к DB </br>
