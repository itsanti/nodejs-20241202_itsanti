# Задание: Реализация фильтрации и пагинации задач

В этом задании вы дополните контроллер и сервис для работы с задачами, добавив функциональность фильтрации задач по статусу и пагинации. Это задание поможет вам освоить обработку запросов с query-параметрами и организацию выборок данных.

---

## Общая структура задачи

Контроллер должен предоставлять следующие функции:

1. **Получение задач с фильтрацией по статусу** – выбор задач с указанным статусом.
2. **Получение задач с пагинацией** – возвращение ограниченного количества задач на одной странице с возможностью выбора страницы.

---

### **Фильтрация задач по статусу**

| Метод | Ссылка | Описание                          | Параметры        |
| ----- | ------ | --------------------------------- | ---------------- |
| GET   | /tasks | Получение списка задач по статусу | `status` (query) |

**Пример запроса**:

```
GET http://localhost:3000/tasks?status=in_progress
```

**Пример ответа**:

```json
[
  {
    "id": "1",
    "title": "Сделать домашнюю работу",
    "description": "Завершить домашнюю работу по программированию",
    "status": "in_progress"
  }
]
```

Если статус указан некорректно (не входит в допустимые значения), сервер должен вернуть ошибку `400`.

---

### **Пагинация задач**

| Метод | Ссылка | Описание                            | Параметры                |
| ----- | ------ | ----------------------------------- | ------------------------ |
| GET   | /tasks | Получение списка задач с пагинацией | `page` и `limit` (query) |

**Пример запроса**:

```
GET http://localhost:3000/tasks?page=1&limit=2
```

**Пример ответа**:

```json
[
  {
    "id": "1",
    "title": "Сделать домашнюю работу",
    "description": "Завершить домашнюю работу по программированию",
    "status": "pending"
  },
  {
    "id": "2",
    "title": "Купить продукты",
    "description": "Купить молоко и хлеб",
    "status": "completed"
  }
]
```

Если параметры `page` и `limit` указаны некорректно (не являются положительными числами), сервер должен вернуть ошибку `400`.

---

### **Фильтрация и пагинация одновременно**

Контроллер также должен поддерживать возможность одновременной фильтрации по статусу и пагинации.

| Метод | Ссылка | Описание                                          | Параметры                          |
| ----- | ------ | ------------------------------------------------- | ---------------------------------- |
| GET   | /tasks | Получение списка задач с фильтрацией и пагинацией | `status`, `page` и `limit` (query) |

**Пример запроса**:

```
GET http://localhost:3000/tasks?status=in_progress&page=1&limit=2
```

**Пример ответа**:

```json
[
  {
    "id": "3",
    "title": "Прочитать книгу",
    "description": "Прочитать 100 страниц книги",
    "status": "in_progress"
  }
]
```

---

## Инструкции

1. **Реализуйте методы фильтрации и пагинации**:

   - В `TasksService` добавьте метод `getTasks`:
     - Обрабатывайте параметры `status`, `page` и `limit`.
     - Фильтруйте задачи по статусу, если параметр `status` указан.
     - Ограничивайте количество возвращаемых задач на одной странице с учетом `page` и `limit`.
   - В `TasksController` вызовите этот метод в обработчике маршрута `GET /tasks`.

2. **Обработка ошибок**:
   - Возвращайте статус `400` для некорректных query-параметров.
   - Возвращайте статус `404`, если задачи не найдены.

---

## Дополнительные (опциональные) задачи

1. **Реализация сортировки**:

   - Добавьте возможность сортировки задач по заголовку или статусу с использованием query-параметра `sortBy`.

   **Пример запроса**:

   ```
   GET http://localhost:3000/tasks?sortBy=title
   ```

---

Этот проект помогает глубже понять работу с query-параметрами, а также базовые принципы фильтрации и пагинации на сервере.