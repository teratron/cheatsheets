# CLI

## `init`

`init` — создает шаблон Prisma-проекта.

- `--datasource-provider` — провайдер для работы с БД: `sqlite`, `postgresql`, `mysql`, `sqlserver` или `mongodb` (перезаписывает `datasource` из `schema.prisma`);
- `--url` — адрес БД (перезаписывает `DATABASE_URL`).

```shell
npx prisma init --datasource-provider mysql --url mysql://user:password@localhost:3306/mydb
```

## `generate`

`generate` — генерирует клиента `Prisma` на основе схемы (`schema.prisma`).

```shell
npx prisma generate
```

## `db pull`

`db pull` — генерирует модели на основе существующей схемы БД.

```shell
npx prisma db pull
```

## `db push`

`db push` — синхронизирует состояние схемы `Prisma` с БД без выполнения миграций.

```shell
npx prisma db push
```

## `seed`

`seed` — выполняет скрипт для наполнения БД начальными (фиктивными) данными. Путь к соответствующему файлу определяется в `package.json`

```json
"prisma": {"seed": "node prisma/seed.js"}
```

```shell
npx prisma seed
```

## `migrate` 

`migrate` — Это приводит к созданию БД при ее отсутствии, генерации файла `prisma/migrations/migration_name.sql`, выполнению инструкции из этого файла (синхронизации БД со схемой) и генерации (регенерации) клиента (`prisma generate`).

- `dev` — выполняет миграцию для разработки;
- `--name` — название миграции.

```shell
npx prisma migrate dev --name init
```

*Данная команда должна выполняться после каждого изменения схемы.*

## `reset`

`reset` — удаляет и заново создает БД или выполняет "мягкий сброс", удаляя все данные, таблицы, индексы и другие артефакты.

```shell
npx prisma migrate reset
```

## `deploy`

`deploy` — выполняет производственную миграцию.

```shell
npx prisma migrate deploy
```

## `studio`

`studio` — позволяет просматривать и управлять данными, хранящимися в БД, в интерактивном режиме.

- `--browser`, `-b` — название браузера (по умолчанию используется дефолтный браузер);
- `--port`, `-p` — номер порта (по умолчанию — `5555`)

```shell
npx prisma studio

# без автоматического открытия вкладки браузера
npx prisma studio -b none
```

---

*Ссылки*: [CLI](https://www.prisma.io/docs/reference/api-reference/command-reference).
