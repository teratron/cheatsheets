# Typescript

## Содержание

- [Переменные и константы](variables.md)
- [Типы данных](types.md)
- [Функции](function.md)
- [О.О.П.](oop.md)
- [S.O.L.I.D](Typescript/solid.md)

## Установка

```shell
# Установка
npm install -g typescript
npm install typescript --save-dev

# Обновление
npm update -g typescript

# Версия
tsc --version
tsc -v
```

## Компиляция

После компиляции в каталоге проекта создается файл **app.js**.

```shell
# Глобально
tsc app.ts

# Локально
npx tsc app.ts

# Автоматическая перекомпиляция
tsc --watch app.ts
tsc -w app.ts

# Версия ECMAScript:
# ES3 (по умолчанию), ES5, ES6 / ES2015, ES7 / ES2016,
# ES2017, ES2018, ES2019, ES2020 или ESNext
tsc app.ts -t ES5

# Удаление комментариев
tsc app.ts --removeComments

# Установка каталога
tsc --outDir D:\ts\js app.ts

# Объединение файлов
tsc --outFile output.js app.ts hello.ts

# Тип модуля
# None, CommonJS (по умолчанию, если ECMAScript ES3 или ES5),
# AMD, System, UMD, ES2015, ES2020 и ESNext
tsc --module commonjs app.ts
tsc -m commonjs app.ts

# Несколько параметров
tsc -t ES5 --outDir js -m commonjs app.ts

# Вызов справки
tsc --help
tsc -h

# Сообщает компилятору, что не надо генерировать файл javascript,
# при возникновении ошибки
tsc --noEmitOnError app.ts
```

```shell

```

```typescript

```

```json

```

---

*Источник*: [Руководство по TypeScript](https://metanit.com/web/typescript)
