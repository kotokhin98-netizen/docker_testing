```markdown
# 🐳 Практическая работа с базой данных MongoDB в Docker

Это пошаговое руководство по работе с **MongoDB** в Docker.  
Мы развернём контейнер с официальным образом `mongo:latest`, научимся подключаться через `mongosh`, выполнять NoSQL-запросы и управлять документами.

👉 [Предыдущая часть с PostgreSQL](./README_POSTGRES.md)

---

## 📋 Предварительные требования

- Установленный **Docker** (версия 20.10+)
- Базовое знакомство с командной строкой
- Порт `27017` на хосте свободен

---

## 🚀 Шаг 1: Запуск контейнера MongoDB

Официальный образ называется **`mongo:latest`**. Запустим контейнер с именем `my-mongo` и пробросим порт.

### Для Linux / macOS / WSL / Git-Bash:
```bash
docker run -d \
  --name my-mongo \
  -p 27017:27017 \
  mongo:latest
```

### Для Windows (PowerShell):
```powershell
docker run -d `
  --name my-mongo `
  -p 27017:27017 `
  mongo:latest
```



**Проверка:**  
```bash
docker ps
```

---

## 🔐 Шаг 2: Подключение к MongoDB

Зайдём внутрь контейнера и подключимся к базе через оболочку `mongosh`.

```bash
docker exec -it my-mongo mongosh
```

> 💡 В MongoDB не требуется пароль для базового подключения в учебном режиме



---

## 🗄️ Шаг 3: Базовые команды mongosh

Выполним простые команды для проверки работы БД.

### Показать все базы данных:
```javascript
show dbs
```


### Создать/выбрать базу данных:
```javascript
use mydb
```

### Показать текущую базу:
```javascript
db
```

### Показать коллекции в текущей базе:
```javascript
show collections
```

### Показать версию MongoDB:
```javascript
version()
```


### Выйти из mongosh:
```javascript
exit
```
или
```javascript
Ctrl+C (дважды)
```

> 💡 MongoDB использует JavaScript-синтаксис, команды не требуют `;` в конце 
![подключение и базывые команды mongosh](/photos/подключение%20и%20базывые%20команды%20mongosh.png)


---

## 📊 Шаг 4: Работа с данными (CRUD)

Создадим коллекцию и поработаем с документами.

### Снова подключаемся:
```bash
docker exec -it my-mongo mongosh
```

### Выбираем базу данных:
```javascript
use mydb
```

### Создаём коллекцию `students` и добавляем документы:
```javascript
db.students.insertMany([
    { name: "Иван Иванов", email: "ivan@example.com", age: 20, course: "ИВТ" },
    { name: "Мария Петрова", email: "maria@example.com", age: 22, course: "ПО" },
    { name: "Алексей Сидоров", email: "alex@example.com", age: 19, course: "ИВТ" }
])
```


### Показать все документы:
```javascript
db.students.find()
```

### Красивый вывод (pretty print):
```javascript
db.students.find().pretty()
```


### Выборка с условием:
```javascript
// Найти студентов старше 20 лет
db.students.find({ age: { $gt: 20 } })

// Найти студентов курса "ИВТ"
db.students.find({ course: "ИВТ" })
```

### Обновление документа:
```javascript
// Обновить возраст Ивана
db.students.updateOne(
    { name: "Иван Иванов" },
    { $set: { age: 21 } }
)
```

### Удаление документа:
```javascript
// Удалить Алексея
db.students.deleteOne({ name: "Алексей Сидоров" })
```

### Подсчёт документов:
```javascript
db.students.countDocuments()
```

### Показать структуру коллекции:
```javascript
db.students.findOne()
```

### Выйти из mongosh:
```javascript
exit
```
![Работа с базой данных mongosh](/photos/Работа%20с%20базой%20данных%20mongosh.png)


---

## 📈 Шаг 5: Мониторинг и логи

### Просмотр логов контейнера:
```bash
docker logs my-mongo
```


### Мониторинг ресурсов в реальном времени:
```bash
docker stats
```
> Выход: `Ctrl+C`


---

## ⚙️ Шаг 6: Управление контейнером

Базовые команды для работы с контейнером:

```bash
# Остановка
docker stop my-mongo

# Запуск снова
docker start my-mongo

# Перезапуск
docker restart my-mongo

# Удаление контейнера
docker rm my-mongo

# Удаление образа (по желанию)
docker rmi mongo:latest
```

---

## 🧹 Шаг 7: Очистка (финал)

После завершения работы удаляем учебные ресурсы.

```bash
# Остановить все контейнеры
docker stop $(docker ps -q)

# Удалить все контейнеры
docker container prune -f

# Удалить неиспользуемые образы
docker image prune -a -f
```

**Проверка очистки:**
```bash
docker ps -a
docker images
```

---


## 💡 Полезные команды MongoDB

```javascript
// Поиск с несколькими условиями
db.students.find({ age: { $gte: 20 }, course: "ИВТ" })

// Сортировка по возрасту (по убыванию)
db.students.find().sort({ age: -1 })

// Ограничение вывода (первые 2 записи)
db.students.find().limit(2)

// Поиск по шаблону (имя начинается на "М")
db.students.find({ name: { $regex: /^М/ } })

// Уникальный индекс на email
db.students.createIndex({ email: 1 }, { unique: true })

// Экспорт коллекции в JSON
// (выполняется вне mongosh, в bash)
docker exec my-mongo mongosh --eval "db.students.find().toArray()" > export.json
```

---

## 🎯 Итог

Вы успешно запустили MongoDB в Docker, подключились через `mongosh`, освоили NoSQL-подход к работе с данными и выполнили основные операции CRUD (Create, Read, Update, Delete). Эти навыки пригодятся при разработке современных приложений с гибкой структурой данных.

**Преимущества MongoDB:**
- 🔹 Гибкая схема данных — легко менять структуру документов
- 🔹 Документная модель — данные хранятся в формате, близком к JSON
- 🔹 Масштабируемость — горизонтальное шардирование "из коробки"
- 🔹 Производительность — быстрые запросы к вложенным данным

---



**Пример файла `scripts/init.js`:**
```javascript
// Инициализация базы данных mydb
db = db.getSiblingDB('mydb');

// Создание коллекции с валидацией
db.createCollection('students', {
    validator: {
        $jsonSchema: {
            bsonType: 'object',
            required: ['name', 'email'],
            properties: {
                name: { bsonType: 'string' },
                email: { 
                    bsonType: 'string',
                    pattern: '^[\\w.+%-]+@[\\w.+%-]+\\.[a-zA-Z]{2,}$'
                },
                age: { bsonType: 'int', minimum: 16, maximum: 100 }
            }
        }
    }
});



