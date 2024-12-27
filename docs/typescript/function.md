# Функции

## Определение функции

```typescript
function add(a: number, b: number) {
    let result = a + b;
    console.log(result);
}

add(20, 30); // 50
```

## Результат функции

```typescript
function add(a: number, b: number): number {
    return a + b;
}

let result = add(1, 2);
```

```typescript
function add(a: number, b: number): void {
    console.log(a + b);
}

add(10, 20);
```

## Необязательные параметры

```typescript
function getName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

let name1 = getName("Иван", "Кузнецов");
console.log(name1); // Иван Кузнецов

let name2 = getName("Вася");
console.log(name2); // Вася
```

```typescript
function getName(firstName: string, lastName: string="Smith") {
    return firstName + " " + lastName;
}

let name1 = getName("Tom");
console.log(name1); // Tom Smith
```

## Тип функции

```typescript
function hello() {
    console.log("Hello TypeScript");
}

const message: () => void = hello;
message();
```

```typescript
function sum(x: number, y: number): number {
    return x + y;
}

function subtract(a: number, b: number): number {
    return a - b;
}

let op: (x: number, y: number) => number;

op = sum;
console.log(op(2, 4));  // 6

op = subtract;
console.log(op(6, 4));  // 2
```

### Функции как параметры других функций

```typescript
function sum(x: number, y: number): number {
    return x + y;
}

function multiply(a: number, b: number): number {
    return a * b;
}

function mathOp(
	x: number,
	y: number,
	op: (a: number, b: number) => number
): number {
    return op(x, y);
}

console.log(mathOp(10, 20, sum));      // 30 
console.log(mathOp(10, 20, multiply)); // 200 
```

```typescript
type Operation = (a: number, b: number) => number;

const sum: Operation = function(x: number, y: number): number {
    return x + y;
};

function mathOp(x: number, y: number, op: Operation): number {
    return op(x, y);
}

console.log(mathOp(10, 20, sum)); // 30
```

## Стрелочные функции

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
