# Лабораторная работа №29. REST API: контроллеры и маршруты

ФИО: Федотова В.С.

Группа: ИСП-232

Дата: 21.04.26

---

## Описание

В ходе данной лабораторной работы было изучено:

- Принципы архитектуры REST и что делает API «RESTful»;

- Контроллеры с полным набором CRUD-маршрутов;

- Разницу между Minimal API и Controller-based API;

- Swagger UI и расширение REST Client в VS Code;

- HTTP-статусы и формат ответов.

## Структура проекта

```
Lab29_RestAPI/
├── TaskApi/
│   ├── Controllers/
│   │   └── TasksController.cs
│   ├── Models/
│   │   ├── TaskItem.cs
│   │   ├── CreateTaskDto.cs
│   │   └── UpdateTaskDto.cs
│   ├── Properties/
│   │   └── launchSettings.json
│   ├── Program.cs
│   ├── requests.http
│   ├── TaskApi.http
│   └── TaskApi.csproj
├── img/
├── .editorconfig
├── .gitignore
├── Lab29_RestAPI.sln
└── README.md
```

## Маршруты

| Метод  | Маршрут                                  | Описание                                  |
| ------ | ---------------------------------------- | ----------------------------------------- |
| GET    | /api/tasks                               | Получить все задачи                       |
| GET    | /api/tasks?completed=true/false          | Фильтрация по статусу                     |
| GET    | /api/tasks/{id}                          | Получить задачу по id                     |
| GET    | /api/tasks/search?query=текст            | Поиск по заголовку/описанию               |
| GET    | /api/tasks/priority/{level}              | Фильтрация по приоритету                  |
| GET    | /api/tasks/stats                         | Статистика (всего/выполнено/не выполнено) |
| GET    | /api/tasks/sorted?by=priority&desc=false | Сортировка по приоритету                  |
| POST   | /api/tasks                               | Создать новую задачу                      |
| PUT    | /api/tasks/{id}                          | Полное обновление задачи                  |
| PATCH  | /api/tasks/{id}/complete                 | Переключить статус выполнения             |
| DELETE | /api/tasks/{id}                          | Удалить задачу                            |

## Итоговая таблица

| Аспект                | ASP.NET Core Controllers           |
| --------------------- | ---------------------------------- |
| Маршруты              | [HttpGet] атрибут над методом      |
| Группировка маршрутов | Класс-контроллер                   |
| Базовый URL           | [Route("api/[controller]")]        |
| Параметр пути         | (int id) — параметр метода         |
| Параметр запроса      | [FromQuery] bool? completed        |
| Тело запроса          | [FromBody] CreateTaskDto dto       |
| Ответ 200             | return Ok(data)                    |
| Ответ 201             | return CreatedAtAction(...)        |
| Ответ 404             | return NotFound(...)               |
| Ответ 204             | return NoContent()                 |
| Типизация данных      | Строгая (C#)                       |
| Документация          | Swagger — устанавливается отдельно |

## Главные выводы

1. REST — не протокол, а архитектурный стиль. Те же принципы работают с любым языком и фреймворком.

2. Контроллер в ASP.NET Core = Router в Express, только с автоматической документацией и строгой типизацией.

3. DTO защищает API от некорректных данных: клиент передаёт только то, что сервер разрешает принять.
4. Swagger UI позволяет тестировать API без Postman и без написания тестового JavaScript-кода.

5. Правильные HTTP-статусы — часть «контракта» API. Клиент должен понимать, что произошло, по коду ответа.
