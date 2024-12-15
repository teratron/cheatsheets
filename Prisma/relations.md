# Отношения

Атрибут `@relation` указывает на существование отношений между моделями (таблицами).

- `name?: string` — название отношения;
- `fields?: [field1, field2, ...fieldN]` — список полей текущей модели (в нашем случае это `[author_id]` модели `Post`); _обратите внимание_: само поле определяется отдельно);
- `references: [field1, field2, ...fieldN]` — список полей другой модели (стороны отношений) (в нашем случае это `[id]` модели `User`).

3 вида отношений:
- один-к-одному (one-to-one, 1-1);
- один-ко-многим (one-to-many, 1-n);
- многие-ко-многим (many-to-many, m-n).

Атрибут `@relation` является обязательным только для отношений `1-1` и `1-n`.

```prisma
model User {
  id      Int      @id @default(autoincrement())
  posts   Post[]
  profile Profile?
}

model Profile {
  id     Int  @id @default(autoincrement())
  user   User @relation(fields: [userId], references: [id])
  userId Int
}

model Post {
  id         Int        @id @default(autoincrement())
  author     User       @relation(fields: [authorId], references: [id])
  authorId   Int
  categories Category[]
}

model Category {
  id    Int    @id @default(autoincrement())
  posts Post[]
}
```

- между моделями `User` и `Profile` существуют отношения `1-1` — у одного пользователя может быть только один профиль;
- между моделями `User` и `Post` существуют отношения `1-n` — у одного пользователя может быть несколько постов;
- между моделями `Post` и `Category` существуют отношения `m-n` — один пост может принадлежать к нескольким категориям, в одну категорию может входить несколько постов.

Подробнее об отношениях можно почитать [здесь](https://www.prisma.io/docs/concepts/components/prisma-schema/relations).
