```markdown
# 🐳 Практическая работа с базой данных PostgreSQL в Docker

Это пошаговое руководство по работе с **PostgreSQL** в Docker.  
Мы развернём контейнер с официальным образом `postgres:alpine`, научимся подключаться к БД, выполнять SQL-запросы и управлять данными.

👉 [Предыдущая часть с MySQL](./README_MYSQL.md)

---

## 📋 Предварительные требования

- Установленный **Docker** (версия 20.10+)
- Базовое знакомство с командной строкой
- Порт `5432` на хосте свободен

---

## 🚀 Шаг 1: Запуск контейнера PostgreSQL

Официальный образ называется **`postgres:alpine`**. Запустим контейнер с именем `my-postgres` и настроим пароль.

### Для Linux / macOS / WSL:
```bash
docker run -d \
  --name my-postgres \
  -p 5432:5432 \
  -e POSTGRES_PASSWORD=mysecretpassword \
  postgres:alpine
```

### Для Windows (PowerShell):
```powershell
docker run -d `
  --name my-postgres `
  -p 5432:5432 `
  -e POSTGRES_PASSWORD=mysecretpassword `
  postgres:alpine
```



**Проверка:**  
```bash
docker ps
```

---

## 🔐 Шаг 2: Подключение к PostgreSQL

Зайдём внутрь контейнера и подключимся к СУБД через `psql`.

```bash
docker exec -it my-postgres psql -U postgres
```

> 💡 Пароль вводить не нужно — мы уже указали его при запуске через `POSTGRES_PASSWORD`



---

## 🗄️ Шаг 3: Базовые команды psql и SQL-запросы

Выполним простые команды для проверки работы БД.

### Показать все базы данных (meta-команда psql):
```sql
\l
```


### Показать пользователей:
```sql
\du
```

### Показать версию PostgreSQL:
```sql
SELECT version();
```


### Показать таблицы в текущей базе:
```sql
\dt
```

### Выйти из psql:
```sql
\q
```

> 💡 Meta-команды psql начинаются с `\`, а обычные SQL-запросы завершаются `;`


![Базовые команды psql и SQL-запросы](../photos/Установка%20и%20работа%20с%20PostgreSQL%20.png)

## 📊 Шаг 4: Работа с данными

Создадим таблицу и поработаем с записями.

### Снова подключаемся к БД:
```bash
docker exec -it my-postgres psql -U postgres
```

### Создаём базу данных для работы:
```sql
CREATE DATABASE mydb;
\c mydb
```

### Создаём таблицу `students`:
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Показать структуру таблицы:
```sql
\d students
```

### Добавляем записи:
```sql
INSERT INTO students (name, email, age) VALUES
    ('Иван Иванов', 'ivan@example.com', 20),
    ('Мария Петрова', 'maria@example.com', 22),
    ('Алексей Сидоров', 'alex@example.com', 19);
```

### Выбираем все записи:
```sql
SELECT * FROM students;
```


### Выборка с условием:
```sql
SELECT name, email FROM students WHERE age > 20;
```

### Обновляем запись:
```sql
UPDATE students SET age = 21 WHERE name = 'Иван Иванов';
```

### Удаляем запись:
```sql
DELETE FROM students WHERE name = 'Алексей Сидоров';
```

### Подсчёт записей:
```sql
SELECT COUNT(*) AS total_students FROM students;
```

### Выйти из psql:
sql
\q

![работа с данными](../photos/Работа%20с%20данными%20в%20postgresSQL.png)

## 📈 Шаг 5: Мониторинг и логи

### Просмотр логов контейнера:
```bash
docker logs my-postgres
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
docker stop my-postgres

# Запуск снова
docker start my-postgres

# Перезапуск
docker restart my-postgres

# Удаление контейнера
docker rm my-postgres

# Удаление образа (по желанию)
docker rmi postgres:alpine
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




---

## 📋 Шпаргалка: PostgreSQL vs MySQL

| Задача | PostgreSQL | MySQL |
|--------|-----------|-------|
| **Образ Docker** | `postgres:alpine` | `mysql:8` |
| **Порт по умолчанию** | 5432 | 3306 |
| **Переменная пароля** | `POSTGRES_PASSWORD` | `MYSQL_ROOT_PASSWORD` |
| **Подключение** | `psql -U postgres` | `mysql -u root -p` |
| **Список БД** | `\l` | `SHOW DATABASES;` |
| **Выбор БД** | `\c dbname` | `USE dbname;` |
| **Список таблиц** | `\dt` | `SHOW TABLES;` |
| **Структура таблицы** | `\d tablename` | `DESCRIBE tablename;` |
| **Выход** | `\q` | `EXIT;` |
| **Автоинкремент** | `SERIAL` | `AUTO_INCREMENT` |



## 🎯 Итог

Вы успешно запустили PostgreSQL в Docker, подключились к базе данных через `psql`, выполнили meta-команды (`\l`, `\dt`, `\d`) и SQL-запросы (CREATE, INSERT, SELECT, UPDATE, DELETE). Эти навыки пригодятся при развёртывании баз данных в любых проектах.




> **Выполнил(а):** `[Ваше ФИО]`  
> **Группа:** `[Ваша группа]`  
> **Дата:** `16.03.2026`
```