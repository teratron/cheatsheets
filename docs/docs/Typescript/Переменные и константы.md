# Переменные и константы

```typescript
var x = "hello";
var x = "work"; // можем определить многократно переменную с одним и тем же именем
```

```typescript
let x = "hello";
let x = "work"; // здесь будет ошибка, так как переменная `x` уже объявлена
```

```typescript
let x = "hello";
var x = "work"; // здесь будет ошибка, так как переменная `x` уже объявлена
```

```typescript
let z = 6;
z = 8; // можем поменять значение на другое
```

```typescript
const z = 6;
z = 8;  // ! Ошибка - нельзя изменить значение константы `z`
```

## Область видимости

```typescript
let x = 10;
{
    let x = 25;
    {
        let x = 163;
        console.log(x); // 163
    }
    console.log(x); // 25
}
console.log(x); // 10
```

```typescript
{
    var x = 94;
    let y = 94;
}
console.log(x); // норм
console.log(y); // ! Ошибка
```

```typescript
console.log(x); // undefined, но норм
var x = 76;

console.log(y); // ! Ошибка
let y = 76;
```

```typescript

```

```typescript

```

```typescript

```

```typescript

```

```typescript

```

```typescript

```
