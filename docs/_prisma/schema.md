# Схема

## `generator`

Генератор клиента на основе схемы.

- `provider` — провайдер генератора (единственным доступным на сегодняшний день провайдером является
  `prisma-client-js`);
- `binaryTargets` — определяет операционную систему для клиента `Prisma`. Значением по умолчанию является `native`, но
  иногда это приходится указывать явно, например, при использовании клиента в `Docker-контейнере` (в этом случае также
  приходится явно выполнять `prisma generate`).

```prisma
generator client {
  provider      = "prisma-client-js"
  binaryTargets = ["native"]
}
```

## `datasource`

Источник данных.

- `provider` — название провайдера для доступа к БД: `sqlite`, `postgresql`, `mysql`, `sqlserver` или `mongodb` (по
  умолчанию — `postgresql`);
- `url` — адрес БД (по умолчанию — значение переменной `DATABASE_URL`);
- `shadowDatabaseUrl` — адрес "теневой" БД (для БД, предоставляемых облачными провайдерами): используется для миграций
  для разработки (`prisma migrate dev`).

```prisma
datasource db {
  provider          = "postgresql"
  url               = env("DATABASE_URL")
  shadowDatabaseUrl = env("SHADOW_DATABASE_URL")
}
```

## `model`

Определим в схеме модели для пользователя (`User`) и поста (`Post`):

```
model User {
  id         String   @id @default(uuid()) @db.Uuid
  email      String   @unique
  hash       String   @map("password_hash")
  first_name String?
  last_name  String?
  age        Int?
  role       Role     @default(USER)
  posts      Post[]
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt

  @@map("users")
}

model Post {
  id         String   @id @default(uuid())
  title      String
  content    String
  published  Boolean
  author_id  String
  author     User     @relation(fields: [author_id], references: [id])
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt

  @@map("posts")
}

enum Role {
  USER
  ADMIN
}
```

## `enum`

Перечисление.
