# Операторы

## `AND`

Все условия должны возвращать `true`.

```javascript
const notPublishedPostsAboutTypeScript = await prisma.post.findMany({
    where: {
        AND: [
            {
                title: {
                    contains: 'TypeScript'
                }
            },
            {
                published: false
            }
        ]
    }
})
```

_Обратите внимание:_ оператор указывается до названия поля (снаружи поля), а фильтр после (внутри).

## `OR`

Хотя бы одно условие должно возвращать `true`.

## `NOT`

Все условия должны возвращать `false`.
