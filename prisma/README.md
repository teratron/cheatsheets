# Prisma

Это современное (продвинутое) [объектно-реляционное отображение](https://ru.wikipedia.org/wiki/ORM) (Object-Relational
Mapping, ORM) для `Node.js` и `TypeScript`.
Это инструмент, позволяющий работать с реляционными (`PostgreSQL`, `MySQL`, `SQL Server`, `SQLite`) и не реляционной (
`MongoDB`) базами данных с помощью `JavaScript` или `TypeScript` без использования `SQL` (хотя такая возможность
имеется).

## Содержание

- Инициализация проекта
- Клиент
- [CLI](cli.md)
- [Схема](schema.md)
- [Типы данных](types.md)
- [Атрибуты](attributes.md)
- [Отношения](relations.md)
- [Запросы](requests.md)
  - [Вложенные запросы](requests.md)
- [Настройки](settings.md)
- [Фильтры](filters.md)
  - [Фильтры для связанных записей](filters.md)
- [Операторы](operators.md)
- [Методы клиента](methods.md)
- [Транзакции](transactions.md)

## Инициализация проекта

```shell
yarn init -yp
# or
npm init -y
```

```shell
yarn add -D prisma
# or
npm i -D prisma
```

```shell
npx prisma init
```

## Клиент

Импортируем и создаем экземпляр клиента Prisma:

```javascript
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

export default prisma
```

Иногда может потребоваться делать так:

```javascript
const Prisma = require('prisma')

const prisma = new Prisma.PrismaClient()

module.exports = prisma
```

---

*Источник*:

- [Prisma docs](https://www.prisma.io/docs/orm/overview/introduction)
- [Prisma Studio](https://www.prisma.io/studio)
- [Prisma ORM: полное руководство для начинающих (и не только). Часть 1](https://habr.com/ru/companies/timeweb/articles/654341/)
- [Prisma ORM: полное руководство для начинающих (и не только). Часть 2](https://habr.com/ru/companies/timeweb/articles/654567/)
