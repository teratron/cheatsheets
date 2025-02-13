# Атрибуты

| Атрибуты     | Описание                                                                                                                                                                                                                                                                              |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `@map`       | привязывает поле схемы (`hash`) к указанной колонке таблицы (`password_hash`). `@map` не меняет название колонки в БД и поля в генерируемом клиенте. Для `MongoDB` использование `@map` для `@id` является обязательным: `id String @default(auto()) @map("_id") @db.ObjectId`        |
| `@db.Uuid`   | тип данных, специфичный для одной или нескольких БД                                                                                                                                                                                                                                   |
| `@id`        | означает, что данное поле является первичным (основным) ключом таблицы (`PRIMARY KEY`) (идентификатор модели). Такое поле не может быть опциональным                                                                                                                                  |
| `@default`   | присваивает полю указанное значение по умолчанию (при отсутствии значения поля) (`DEFAULT`). Дефолтными могут быть статические значения (`42`, `hi`) или значения, генерируемые функциями `autoincrement`, `dbgenerated`, `cuid`, `uuid` и `now` (функции атрибутов; см. ниже)        |
| `@unique`    | означает, что значение поля должно быть уникальным в пределах таблицы (`UNIQUE`). Таблица должна иметь хотя бы одно поле `@id` или `@unique`                                                                                                                                          |
| `@relation`  | указывает на существование отношений между таблицами. В данном случае между таблицами `users` и `posts` существуют отношения один-ко-многим (one-to-many, 1-n) — у одного пользователя может быть несколько постов (`FOREIGN KEY / REFERENCES`) (об отношениях мы поговорим отдельно) |
| `@updatedAt` | обновляет поле текущими датой и временем при любой модификации записи                                                                                                                                                                                                                 |
| `@ignore`    | используется для обозначения не валидных полей                                                                                                                                                                                                                                        |
| `@@map`      | привязывает название модели к названию таблицы в БД. `@@map` не меняет название таблицы в БД и модели в генерируемом клиенте                                                                                                                                                          |
| `@@id`       | определяет составной (composite) первичный ключ таблицы, например, `@@id[title, author]` (в данном случае соответствующее поле будет называться `title_author` — это можно изменить)                                                                                                  |
| `@@unique`   | определяет составное ограничение уникальности (unique constraint) для указанных полей (такие поля не могут быть опциональными), например, `@@unique([title, author])`                                                                                                                 |
| `@@index`    | определяет индекс в БД (`INDEX`), например, `@@index([title, author])`                                                                                                                                                                                                                |
| `@@ignore`   | используется для обозначения не валидных моделей                                                                                                                                                                                                                                      |

## Функции атрибутов

| Функции         | Описание                                                                                                            |
|-----------------|---------------------------------------------------------------------------------------------------------------------|
| `auto`          | представляет дефолтные значения, генерируемые БД (только для `MongoDB`)                                             |
| `autoincrement` | генерирует последовательные целые числа (`SERIAL` в `PostgreSQL`, не поддерживается `MongoDB`)                      |
| `cuid`          | генерирует глобальный уникальный идентификатор на основе спецификации [`cuid`](https://github.com/ericelliott/cuid) |
| `uuid`          | генерирует глобальный уникальный идентификатор на основе спецификации [`UUID`](https://ru.wikipedia.org/wiki/UUID)  |
| `now`           | возвращает текущую отметку времени (timestamp) (`CURRENT_TIMESTAMP` в `PostgreSQL`)                                 |
| `dbgenerated`   | представляет дефолтные значения, которые не могут быть выражены в схеме (например, `random()`)                      |

## Префиксы

- `@` — означает атрибут поля;
- `@@` — атрибут блока (модели, таблицы).

## Модификаторы

- `?` после названия типа означает, что данное поле является опциональным (необязательным, может иметь значение `NULL`);
- `[]` после названия типа означает, что значением данного поля является список (массив). Такое поле не может быть
  опциональным;