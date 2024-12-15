# Prisma

`Prisma` — это современное (продвинутое) [объектно-реляционное отображение](https://ru.wikipedia.org/wiki/ORM) (Object-Relational Mapping, ORM) для `Node.js` и `TypeScript`. Проще говоря, `Prisma` — это инструмент, позволяющий работать с реляционными (`PostgreSQL`, `MySQL`, `SQL Server`, `SQLite`) и не реляционной (`MongoDB`) базами данных с помощью `JavaScript` или `TypeScript` без использования [`SQL`](https://ru.wikipedia.org/wiki/SQL) (хотя такая возможность имеется).

## Содержание

- Инициализация проекта
- Клиент
- [CLI](cli.md)
- [Схема](schema.md)
- Типы данных
- [Атрибуты](attributes.md)
- [Отношения](relations.md)
- [Запросы](requests.md)

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

Импортируем и создаем экземпляр клиента `Prisma`:

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

## Типы данных

- `String` — строка переменной длины (для `PostgreSQL` — это тип `text`);
- `Boolean` — логическое значение: `true` или `false` (`boolean`);
- `Int` — целое число (`integer`);
- `BigInt` — [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) (`integer`);
- `Float` — число с плавающей точкой (запятой) (`double precision`);
- `Decimal` (`decimal(65,30)`);
- `DateTime` — дата и время в формате [`ISO 8601`](https://ru.wikipedia.org/wiki/ISO_8601);
- `Json` — объект в формате `JSON` (`jsonb`);
- `Bytes` (`bytea`).

Атрибут `@db` позволяет использовать типы данных, специфичные для одной или нескольких БД.


```shell

```

```prisma

```

---

*Источник*: 
- [Prisma docs](https://www.prisma.io/docs/orm/overview/introduction)
- [Prisma Studio](https://www.prisma.io/studio)
- [Prisma ORM: полное руководство для начинающих (и не только). Часть 1](https://habr.com/ru/companies/timeweb/articles/654341/)
- [Prisma ORM: полное руководство для начинающих (и не только). Часть 2](https://habr.com/ru/companies/timeweb/articles/654567/)
