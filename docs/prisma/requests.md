# Запросы

## `findUnique`

Позволяет извлекать единичные записи по идентификатору или уникальному полю.

**Сигнатура**

```javascript
findUnique({
    where: condition,
  select? : fields,
  include? : relations,
  rejectOnNotFound? : boolean
})
```

Модификатор`?`означает, что поле является опциональным.

- `condition`— условие для выборки;
- `fields`— поля для выборки;
- `relations`— отношения (связанные поля) для выборки;
- `rejectOnNotFound`— если имеет значение`true`, при отсутствии записи выбрасывается исключение`NotFoundError`. Если
  имеет значение`false`, при отсутствии записи возвращается`null`.

**Пример**

```javascript
async function getUserById(id) {
    try {
        const user = await prisma.user.findUnique({
          where: {
            id
          }
        })
        return user
    } catch (e) {
        onError(e)
    }
}
```

## `findFirst`

Возвращает первую запись, соответствующую заданному критерию.

**Сигнатура**

```javascript
findFirst({
  where? : condition,
  select? : fields,
  include? : relations,
  rejectOnNotFound? : boolean,
  distinct? : field,
  orderBy? : order,
  cursor? : position,
  skip? : number,
  take? : number
})
```

- `distinct`— фильтрация по определенному полю;
- `orderBy`— сортировка по определенному полю и в определенном порядке;
- `cursor`— позиция начала списка (как правило,`id`или другое уникальное значение);
- `skip`— количество пропускаемых записей;
- `take`— количество возвращаемых записей (в данном случае может иметь значение `1` или `-1`: во втором случае
  возвращается
  последняя запись).

**Пример**

```javascript
async function getLastPostByAuthorId(author_id) {
    try {
        const post = await prisma.post.findFirst({
          where: {
            author_id
          },
          orderBy: {
            created_at: 'asc'
          },
            take: -1
        })
        return post
    } catch (e) {
        onError(e)
    }
}
```

## `findMany`

Возвращает все записи, соответствующие заданному критерию.

**Сигнатура**

```javascript
findMany({
  where? : condition,
  select? : fields,
  include? : relations,
  rejectOnNotFound? : boolean,
  distinct? : field,
  orderBy? : order,
  cursor? : position,
  skip? : number,
  take? : number
})
```

**Пример**

```javascript
async function getAllPostsByAuthorId(author_id) {
    try {
        const posts = await prisma.post.findMany({
          where: {
            author_id
          },
          orderBy: {
            updated_at: 'desc'
          }
        })
        return posts
    } catch (e) {
        onError(e)
    }
}
```

## `create`

Создает новую запись.

**Сигнатура**

```javascript
create({
  data: _data,
  select? : fields,
  include? : relations
})
```

- `_data`— данные создаваемой записи.

**Пример**

```javascript
async function createUserWithProfile(data) {
    const {email, password, firstName, lastName, age} = data
    try {
        const hash = await argon2.hash(password)
        const user = await prisma.user.create({
            data: {
                email,
                hash,
                profile: {
                    create: {
                        first_name: firstName,
                        last_name: lastName,
                        age
                    }
                }
            },
          select: {
            email: true
          },
          include: {
            profile: true
          }
        })
        return user
    } catch (e) {
        onError(e)
    }
}
```

## `update`

Обновляет существующую запись.

**Сигнатура**

```javascript
update({
  data: _data,
  where: condition,
  select? : fields,
  include? : relations
})
```

**Пример**

```javascript
async function updateUserById(id, changes) {
    const {email, age} = changes
    try {
        const user = await prisma.user.update({
          where: {
            id
          },
            data: {
                email,
                profile: {
                  update: {
                    age
                  }
                }
            },
          select: {
            email: true
          },
          include: {
            profile: true
          }
        })
        return user
    } catch (e) {
        onError(e)
    }
}
```

## `upsert`

Обновляет существующую или создает новую запись.

**Сигнатура**

```javascript
upsert({
  create: _data,
  update: _data,
  where: condition,
  select? : fields,
  include? : relations
})
```

**Пример**

```javascript
async function updateOrCreateUser(data) {
    const {userName, email, password} = data
    try {
        const hash = await argon2.hash(password)
        const user = await prisma.user.create({
          where: {
            user_name: userName
          },
          update: {
            email,
            hash
          },
          create: {
            email,
            hash,
            user_name: userName
          },
          select: {
            user_name: true,
            email: true
          }
        })
        return user
    } catch (e) {
        onError(e)
    }
}
```

## `delete`

Удаляет существующую запись по идентификатору или уникальному полю.

**Сигнатура**

```javascript
delete ({
  where: condition,
  select? : fields,
  include? : relations
})
```

**Пример**

```javascript
async function removeUserById(id) {
    try {
      await prisma.user.delete({
        where: {
          id
        }
      })
    } catch (e) {
        onError(e)
    }
}
```

## `createMany`

Создает несколько записей с помощью одной транзакции (о транзакциях мы поговорим отдельно).

**Пример**

```javascript
createMany({
    data: _data[],
  skipDuplicates? : boolean
})
```

- `_data[]`— данные для создаваемых записей в виде массива;
- `skipDuplicates`— при значении`true`создаются только уникальные записи.

**Пример**

```javascript
// предположим, что `users` - это массив объектов
async function createUsers(users) {
    try {
      const users = await prisma.user.createMany({
        data: users
      })
        return users
    } catch (e) {
        onError(e)
    }
}
```

## `updateMany`

Обновляет несколько существующих записей за один раз и возвращает количество (sic) обновленных записей.

**Сигнатура**

```javascript
updateMany({
    data: _data[],
  where? : condition
})
```

**Пример**

```javascript
async function updateProductsByCategory(category, newDiscount) {
    try {
        const count = await prisma.product.updateMany({
          where: {
            category
          },
          data: {
            discount: newDiscount
          }
        })
        return count
    } catch (e) {
        onError(e)
    }
}
```

## `deleteMany`

Удаляет несколько записей с помощью одной транзакции и возвращает количество удаленных записей.

**Сигнатура**

```javascript
deleteMany({
  where? : condition
})
```

**Пример**

```javascript
async function removeAllPostsByUserId(author_id) {
    try {
        const count = await prisma.post.deleteMany({
          where: {
            author_id
          }
        })
        return count
    } catch (e) {
        onError(e)
    }
}
```

## `count`

Возвращает количество записей, соответствующих заданному критерию.

**Сигнатура**

```javascript
count({
  where? : condition,
  select? : fields,
  cursor? : position,
  orderBy? : order,
  skip? : number,
  take? : number
})
```

**Пример**

```javascript
async function countUsersWithPublishedPosts() {
    try {
        const count = await prisma.user.count({
            where: {
                post: {
                    some: {
                        published: true
                    }
                }
            }
        })
        return count
    } catch (e) {
        onError(e)
    }
}
```

## `aggregate`

Выполняет агрегирование полей.

**Сигнатура**

```javascript
aggregate({
  where? : condition,
  select? : fields,
  cursor? : position,
  orderBy? : order,
  skip? : number,
  take? : number,
    _count: count,
    _avg: avg,
    _sum: sum,
    _min: min,
    _max: max
})
```

- `_count`— возвращает количество совпадающих записей или не`null-полей`;
- `_avg`— возвращает среднее значение определенного поля;
- `_sum`— возвращает сумму значений определенного поля;
- `_min`— возвращает наименьшее значение определенного поля;
- `_max`— возвращает наибольшее значение определенного поля.

**Пример**

```javascript
async function getAllUsersCountAndMinMaxProfileViews() {
    try {
        const result = await prisma.user.aggregate({
          _count: {
            _all: true
          },
          _max: {
            profileViews: true
          },
          _min: {
            profileViews: true
          }
        })
        return result
    } catch (e) {
        onError(e)
    }
}
```

## `groupBy`

Выполняет группировку полей.

**Сигнатура**

```javascript
groupBy({
  by? : by,
  having? : having,
  where? : condition,
  orderBy? : order,
  skip? : number,
  take? : number,
    _count: count,
    _avg: avg,
    _sum: sum,
    _min: min,
    _max: max
})
```

- `by`— определяет поле или комбинацию полей для группировки записей;
- `having`— позволяет фильтровать группы по агрегируемому значению.

**Пример**

В следующем примере мы выполняем группировку по`country / city`, где среднее значение`profileViews`превышает`100`, и
возвращаем общее количество (`_sum`)`profileViews`для каждой группы. Запрос также возвращает количество всех (`_all`)
записей в каждой группе и все записи с не`null`значениями поля`city`в каждой группе:

```javascript
async function getUsers() {
    try {
        const result = await prisma.user.groupBy({
            by: ['country', 'city'],
          _count: {
            _all: true,
            city: true
          },
          _sum: {
            profileViews: true
          },
          orderBy: {
            country: 'desc'
          },
          having: {
            profileViews: {
              _avg: {
                gt: 100
              }
            }
          }
        })
        return result
    } catch (e) {
        onError(e)
    }
}
```

## Вложенные запросы

### `create`

`create: { data } | [{ data1 }, { data2 }, ...{ dataN }]` — добавляет новую связанную запись или набор записей в
родительскую запись. `create` доступен при создании (`create`) новой родительской записи или обновлении (`update`)
существующей родительской записи.

```javascript
const user = await prisma.user.create({
  data: {
    email,
    profile: {
      // вложенный запрос
      create: {
        first_name,
        last_name
      }
    }
  }
})
```

### `createMany`

`createMany: [{ data1 }, { data2 }, ...{ dataN }]` — добавляет набор новых связанных записей в родительскую запись.
createMany доступен при создании (`create`) новой родительской записи или обновлении (`update`) существующей
родительской записи.

```javascript
const userWithPosts = await prisma.user.create({
  data: {
    email,
    posts: {
      // !
      createMany: {
        data: posts
      }
    }
  }
})
```

### `update`

`update: { data } | [{ data1 }, { data2 }, ...{ dataN }]` — обновляет одну или более связанных записей.

```javascript
const user = await prisma.user.update({
  where: {
    email
  },
  data: {
    profile: {
      // !
      update: {
        age
      }
    }
  }
})
```

### `updateMany`

`updateMany: { data } | [{ data1 }, { data2 }, ...{ dataN }]` — обновляет массив связанных записей. Поддерживается
фильтрация.

```javascript
const result = await prisma.user.update({
  where: {
    id
  },
  data: {
    posts: {
      // !
      updateMany: {
        where: {
          published: false
        },
        data: {
          like_count: 0
        }
      }
    }
  }
})
```

### `upsert`

`upsert: { data } | [{ data1 }, { data2 }, ...{ dataN }]` — обновляет существующую связанную запись или создает новую.

```javascript
const user = await prisma.user.update({
  where: {
    email
  },
  data: {
    profile: {
      // !
      upsert: {
        create: {
          age
        },
        update: {
          age
        }
      }
    }
  }
})
```

### `delete`

`delete: boolean | { data } | [{ data1 }, { data2 }, ...{ dataN }]` — удаляет связанную запись. Родительская запись при
этом не удаляется.

```javascript
const user = await prisma.user.update({
  where: {
    email
  },
  data: {
    profile: {
      delete: true
    }
  }
})
```

### `deleteMany`

`deleteMany: { data } | [{ data1 }, { data2 }, ...{ dataN }]` — удаляет связанные записи. Поддерживается фильтрация.

```javascript
const user = await prisma.user.update({
  where: {
    id
  },
  data: {
    age,
    posts: {
      // !
      deleteMany: {}
    }
  }
})
```

### `set`

`set: { data } | [{ data1 }, { data2 }, ...{ dataN }]` — перезаписывает значение связанной записи.

```javascript
const userWithPosts = await prisma.user.update({
  where: {
    email
  },
  data: {
    posts: {
      // !
      set: newPosts
    }
  }
})
```

### `connect`

Подключает запись к существующей связанной записи по идентификатору или уникальному полю.

```javascript
const user = await prisma.post.create({
  data: {
    title,
    content,
    author: {
      connect: {
        email
      }
    }
  }
})
```

### `connectOrCreate`

Подключает запись к существующей связанной записи по идентификатору или уникальному полю либо создает связанную запись
при отсутствии таковой.

### `disconnect`

Отключает родительскую запись от связанной без удаления последней. `disconnect` доступен только если отношение является
опциональным.
