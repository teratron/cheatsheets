# Настройки

## `select`

Определяет, какие поля включаются в возвращаемый объект.

```javascript
const user = await prisma.user.findUnique({
    where: {
        email
    },
    select: {
        id: true,
        email: true,
        first_name: true,
        last_name: true,
        age: true
    }
})

// or
const usersWithPosts = await prisma.user.findMany({
    select: {
        id: true,
        email: true,
        posts: {
            select: {
                id: true,
                title: true,
                content: true,
                author_id: true,
                created_at: true
            }
        }
    }
})

// or
const usersWithPostsAndComments = await prisma.user.findMany({
    select: {
        id: true,
        email: true,
        posts: {
            include: {
                comments: true
            }
        }
    }
})
```

## `include`

Определяет, какие отношения (связанные записи) включаются в возвращаемый объект.

```javascript
const userWithPostsAndComments = await prisma.user.findUnique({
    where: {
        email
    },
    include: {
        posts: true,
        comments: true
    }
})
```

## `where`

Определяет один или более фильтр, применяемый к свойствам записи или связанных записей.

```javascript
const admins = await prisma.user.findMany({
    where: {
        email: {
            contains: 'admin'
        }
    }
})
```

## `orderBy`

Определяет поля и порядок сортировки. Возможными значениями `orderBy` являются `asc` и `desc`.

```javascript
const usersByPostCount = await prisma.user.findMany({
    orderBy: {
        posts: {
            count: 'desc'
        }
    }
})
```

## `distinct`

Определяет поля, которые должны быть уникальными в возвращаемом объекте.

```javascript
const distinctCities = await prisma.user.findMany({
    select: {
        city: true,
        country: true
    },
    distinct: ['city']
})
```
