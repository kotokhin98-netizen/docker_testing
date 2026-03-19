```markdown
# 🐳 Практическая работа с базой данных MySQL в Docker

Это пошаговое руководство по работе с **MySQL** в Docker.  
Мы развернём контейнер с официальный образом `mysql:8`, научимся подключаться к БД, выполнять SQL-запросы и управлять данными.

👉 [Предыдущая часть с Apache](./README_APACHE.md)

---

## 📋 Предварительные требования

- Установленный **Docker** (версия 20.10+)
- Базовое знакомство с командной строкой
- Порт `3306` на хосте свободен

---

## 🚀 Шаг 1: Запуск контейнера MySQL

Официальный образ называется **`mysql:8`**. Запустим контейнер с именем `my-mysql` и настроим переменные окружения.

### Для Linux / macOS / WSL:
```bash
docker run -d \
  --name my-mysql \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=rootpassword \
  -e MYSQL_DATABASE=mydb \
  -e MYSQL_USER=user \
  -e MYSQL_PASSWORD=password \
  mysql:8
```

### Для Windows (PowerShell):
```powershell
docker run -d `
  --name my-mysql `
  -p 3306:3306 `
  -e MYSQL_ROOT_PASSWORD=rootpassword `
  -e MYSQL_DATABASE=mydb `
  -e MYSQL_USER=user `
  -e MYSQL_PASSWORD=password `
  mysql:8
```

![Запуск контейнера](../photos/)

**Проверка:**  
```bash
docker ps
```

---

## 🔐 Шаг 2: Подключение к MySQL

Зайдём внутрь контейнера и подключимся к СУБД.

```bash
docker exec -it my-mysql mysql -u root -p
```

**Пароль:** `rootpassword`

> 💡 При вводе пароля символы не отображаются — это нормально! Просто введите и нажмите Enter.

![Подключение к MySQL](../photos/Подключение%20к%20базе%20данных.png)

---

## 🗄️ Шаг 3: Базовые SQL-запросы

Выполним простые команды для проверки работы БД.

### Показать все базы данных:
```sql
SHOW DATABASES;
```

### Выбрать базу данных:
```sql
USE mydb;
```

### Показать версию MySQL:
```sql
SELECT VERSION();
```

### Показать таблицы в текущей базе:
```sql
SHOW TABLES;
```

### Выйти из MySQL:
```sql
EXIT;
```
![Выполнение запросов SQL ](../photos/Выполнение%20SQL-запросов.png)

> 💡 Все SQL-команды завершаются точкой с запятой `;`

---

## 📊 Шаг 4: Работа с данными

Создадим таблицу и поработаем с записями.

### Снова подключаемся к БД:
```bash
docker exec -it my-mysql mysql -u root -p
```

### Выбираем базу:
```sql
USE mydb;
```

### Создаём таблицу `students`:
```sql
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
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

### Обновляем запись:
```sql
UPDATE students SET age = 21 WHERE name = 'Иван Иванов';
```

### Удаляем запись:
```sql
DELETE FROM students WHERE name = 'Алексей Сидоров';
```

### Выйти из MySQL:
```sql
EXIT;
```

![Работа с данными ](../photos/Работа%20с%20данными.png)


## 📈 Шаг 5: Мониторинг и логи

### Просмотр логов контейнера:
```bash
docker logs my-mysql
```

### Мониторинг ресурсов в реальном времени:
```bash
docker stats
```
> Выход: `Ctrl+C`


## ⚙️ Шаг 6: Управление контейнером

Базовые команды для работы с контейнером:

```bash
# Остановка
docker stop my-mysql

# Запуск снова
docker start my-mysql

# Перезапуск
docker restart my-mysql

# Удаление контейнера
docker rm my-mysql

# Удаление образа (по желанию)
docker rmi mysql:8
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




## 🎯 Итог

Вы успешно запустили MySQL в Docker, подключились к базе данных, выполнили SQL-запросы (CREATE, INSERT, SELECT, UPDATE, DELETE) и освоили базовое управление контейнером. Эти навыки пригодятся при развёртывании баз данных в любых проектах.



> **Выполнил(а):** `[Котохин Артем Ильич]`  
> **Группа:** `[28Ипо8482]`  
> **Дата:** `16.03.2026`
