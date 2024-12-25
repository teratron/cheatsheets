# Фильтры

## `equals`

Значение равняется `n`.

```javascript
const usersWithNameHarry = await prisma.user.findMany({
    where: {
        name: {
            equals: 'Harry'
        }
    }
})

// `equals` может быть опущено
const usersWithNameHarry = await prisma.user.findMany({
    where: {
        name: 'Harry'
    }
})
```

## `not`

Значение не равняется `n`.

## `in`

Значение `n` содержится в списке (массиве).

```javascript
const usersWithNameAliceOrBob = await prisma.user.findMany({
    where: {
        user_name: {
            // !
            in: ['Alice', 'Bob']
        }
    }
})
```

## `notIn`

`n` не содержится в списке.

## `lt`

`n` меньше `x`.

```javascript
const notPopularPosts = await prisma.post.findMany({
    where: {
        likeCount: {
            lt: 100
        }
    }
})
```

## `lte`

`n` меньше или равно `x`.

## `gt`

`n` больше `x`.

## `gte`

`n` больше или равно `x`.

## `contains`

`n` содержит `x`.

```javascript
const admins = await prisma.user.findMany({
    where: {
        email: {
            contains: 'admin'
        }
    }
})
```

## `startsWith`

`n` начинается с `x`.

```javascript
const usersWithNameStartsWithA = await prisma.user.findMany({
    where: {
        user_name: {
            startsWith: 'A'
        }
    }
})
```

## `endsWith`

`n` заканчивается `x`.

## Фильтры для связанных записей

### `some`

Возвращает все связанные записи, соответствующие одному или более критерию фильтрации.

```javascript
const usersWithPostsAboutTypeScript = await prisma.user.findMany({
    where: {
        posts: {
            some: {
                title: {
                    contains: 'TypeScript'
                }
            }
        }
    }
})
```

### `every`

Возвращает все связанные записи, соответствующие всем критериям.

### `none`

Возвращает все связанные записи, не соответствующие ни одному критерию.

### `is`

Возвращает все связанные записи, соответствующие критерию.

### `notIs`

Возвращает все связанные записи, не соответствующие критерию.
