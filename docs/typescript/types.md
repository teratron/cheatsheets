# Типы данных

| Тип         | Описание                                                                                                           |
|-------------|--------------------------------------------------------------------------------------------------------------------|
| `boolean`   | логическое значение `true` или `false`                                                                             |
| `number`    | числовое значение                                                                                                  |
| `string`    | строки                                                                                                             |
| `Array`     | массивы                                                                                                            |
| `Tuple`     | кортежи                                                                                                            |
| `Enum`      | перечисления                                                                                                       |
| `Any`       | произвольный тип                                                                                                   |
| `Symbol`    |                                                                                                                    |
| `Never`     | отсутствие значения и используется в качестве возвращаемого типа функций, которые генерируют или возвращают ошибку |
| `null`      | соответствуют значениям `null` в javascript                                                                        |
| `undefined` | соответствуют значениям `undefined` в javascript                                                                   |

```typescript
let x: number = 10; 
let hello: string = "hello world";
let isValid: boolean = true;

hello = 23; // ! Ошибка
```

## `boolean`

```typescript
let isEnabled: boolean = true;
let isAlive: boolean = false;
```

## `number`

```typescript
let decimal: number = 6;

// шестнадцатиричная система
let hex: number = 0xf00d;       // 61453 в десятичной

// двоичная система
let binary: number = 0b1010;    // 10 в десятичной

// восьмиричная система
let octal: number = 0o744;      // 484 в десятичной
```

## `string`

```typescript
let firstName: string = "Tom";
let lastName = 'Johns';
```

### Шаблон строк

```typescript
let firstName: string = "Tom";
let age: number = 28;

let info: string = `Имя ${firstName}    Возраст: ${age}`;
console.log(info);  // Имя Tom    Возраст: 28

let sentence: string = `Hello World!
Good bye World!`; // многострочный текст
```

## `bigint`

Для представления очень больших чисел.

```typescript
const num1: bigint = BigInt(100);
// или
const num2: bigint = 100n;
```

Следует отметить, что этот тип - часть стандарта ES2020, поэтому при компиляции следует установить данный стандарт в
качестве целевого через параметр`target` в файле`tsconfig.json`:

```json
{
    "compilerOptions": {
        "target": "es2020",
        "outFile": "app.js"
    }
}
```

## `any`

```typescript
let someVar: any = "hello";
console.log(someVar);   // сейчас someVar - это string

someVar = 20;
console.log(someVar);   // сейчас someVar - это number

var someArray: any[] = [24, "Tom", false];
```

```typescript
let x;  // тип any
x = 10;
x = "hello";
```

## Проверка типа

```typescript
let sum: any;
sum = 1200;

if (typeof sum === "number") {
    let result: number = sum / 12;
    console.log(result);
} else {
    console.log("invalid operation");
}
```

Оператор`typeof`может возвращать следующие значения:

- `string`
- `number`
- `bigint`
- `boolean`
- `symbol`
- `undefined`
- `object`
- `function`
