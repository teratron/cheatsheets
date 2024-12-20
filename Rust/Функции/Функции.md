*Теги*: [[Rust]], [[Функции]], [[Методы]]

```rust
fn main() {
    fizzbuzz_to(100);
}

// Функция, которая возвращает булево значение
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    if rhs == 0 {
        return false;
    }

    // Это выражение, ключевое слово `return` здесь не требуется
    lhs % rhs == 0
}

// Функции которые "не" возвращают значение, на самом деле возвращают единичный тип `()`
fn fizzbuzz(n: u32) -> () {
    if is_divisible_by(n, 15) {
        println!("fizzbuzz");
    } else if is_divisible_by(n, 3) {
        println!("fizz");
    } else if is_divisible_by(n, 5) {
        println!("buzz");
    } else {
        println!("{}", n);
    }
}

// Если функция возвращает `()`, тип возвращаемого значения можно не указывать
// в сигнатуре
fn fizzbuzz_to(n: u32) {
    for n in 1..=n {
        fizzbuzz(n);
    }
}
```

## Связанные функции и Методы

**Связанные функции** — это функции, которые обычно определены для типа в целом.

**Методы** — это связанные функции, которые вызываются для конкретного экземпляра типа.

```rust
struct Point {
    x: f64,
    y: f64,
}

// Блок реализации, все функции и методы,
// связанные с типом `Point` размещаются здесь
impl Point {
    // Это "связанная функция", так как эта функция связана
    // с конкретным типом, в данном случае, Point.
    //
    // Связанные функции не обязательно вызывать с каким-то экземпляром класса.
    // Чаще всего такие функции используются как конструкторы.
    fn origin() -> Point {
        Point { x: 0.0, y: 0.0 }
    }

    // Ещё одны связанная функция, принимающая два аргумента:
    fn new(x: f64, y: f64) -> Point {
        Point { x: x, y: y }
    }
}

struct Rectangle {
    p1: Point,
    p2: Point,
}

impl Rectangle {
    // Это метод
    // `&self` - это синтаксический сахар для замены `self: &Self`,
    // где `Self` - это тип вызывающего объекта
    // В данном случае `Self` = `Rectangle`
    fn area(&self) -> f64 {
        // `self` предоставляет доступ к полям структуры
        // с помощью оператора "точка"
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        ((x1 - x2) * (y1 - y2)).abs()
    }

    fn perimeter(&self) -> f64 {
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        2.0 * ((x1 - x2).abs() + (y1 - y2).abs())
    }

    // Этот метод требует, чтобы вызывающий объект был изменяемым
    // `&mut self` преобразуется в `self: &mut Self`
    fn translate(&mut self, x: f64, y: f64) {
        self.p1.x += x;
        self.p2.x += x;

        self.p1.y += y;
        self.p2.y += y;
    }
}

// `Pair` владеет ресурсами: двумя целыми числами,
// память для которых выделена в куче
struct Pair(Box<i32>, Box<i32>);

impl Pair {
    // Этот метод "потребляет" ресурсы вызывающего объекта
    // `self` преобразуется в  `self: Self`
    fn destroy(self) {
        // Деструктуризируем `self`
        let Pair(first, second) = self;

        println!("Удаляем Pair({}, {})", first, second);

        // `first` и `second` выходят за пределы области видимости и удаляются
    }
}

fn main() {
    let rectangle = Rectangle {
        // Связанные функции вызываются с помощью двойных двоеточий
        p1: Point::origin(),
        p2: Point::new(3.0, 4.0),
    };

    // Методы вызываются с помощью оператора "точка"
    // Обратите внимание, что первый аргумент `&self` передаётся неявно, т.е.
    // `rectangle.perimeter()` === `Rectangle::perimeter(&rectangle)`
    println!("Периметр прямоугольника: {}", rectangle.perimeter());
    println!("Площадь прямоугольника: {}", rectangle.area());

    let mut square = Rectangle {
        p1: Point::origin(),
        p2: Point::new(1.0, 1.0),
    };
    // Ошибка! `rectangle` неизменяемый, но в методе требуется изменяемый объект

    // Изменяемые объекты могут вызывать изменяемые методы
    square.translate(1.0, 1.0);

    let pair = Pair(Box::new(1), Box::new(2));

    pair.destroy();
    
    // Ошибка! Предыдущий вызов `destroy` "употребил" переменную `pair`
    //pair.destroy();
    // TODO ^ Попробуйте раскомментировать эту строку
}
```

```rust

```

```rust

```

```rust

```

```rust

```

```rust

```

```rust

```
