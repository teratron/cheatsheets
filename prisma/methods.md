# Методы клиента

## `$connect`

Открывает соединение с БД.

## `$disconnect`

Закрывает соединение с БД, и останавливает движок запросов (query engine) Prisma.

```javascript
import {PrismaClient} from '@prisma/client'

const prisma = new PrismaClient()

async function seedDb() {
    try {
        await prisma.model.create(data)
    } catch (e) {
        onError(e)
    } finally {
        // !
        await prisma.$disconnect()
    }
}
```

## `$use`

Добавляет посредника (middleware).

```javascript
prisma.$use(async (params, next) => {
    console.log('Это посредник')

    // работаем с `params`

    return next(params)
})
```

- `next` — представляет "следующий уровень" в стеке посредников. Таким уровнем может быть следующий посредник или движок
  запросов Prisma;
- `params` — объект со следующими свойствами:
    - `action` — тип запроса, например, `create` или `findMany`;
    - `args` — аргументы, переданные в запрос, например, `where` или `data`;
    - `model` — модель, например, `User` или `Post`;
    - `runInTransaction` — возвращает `true`, если запрос был запущен в контексте транзакции.

## `$queryRaw`, `$executeRaw` и `$runCommandRaw`

Предназначены для работы с SQL.

## `$transaction`

Выполняет запросы в контексте [транзакции](transactions.md).
