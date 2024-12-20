
*Теги*: [[Rust]], [[Форматированный вывод]]

```rust
#![allow(unused)]

fn main() {
	use std::fmt;
	
	struct Structure(i32);
	
	// Чтобы была возможность использовать маркер `{}`
	// `типаж (trait) fmt::Display` должен быть реализован вручную
	// для данного типа.
	impl fmt::Display for Structure {
	    // Этот типаж требует реализацию метода `fmt` с данной сигнатурой:
	    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
	        // Записываем первый элемент в выходной поток `f`.
	        // Возвращаем `fmt::Result`, который показывает выполнилась
	        // операция успешно или нет.
	        // Обратите внимание на то, что синтаксис `write!`
	        // похож на синтаксис `println!`.
	        write!(f, "{}", self.0)
	    }
	}
}
```

```rust
use std::fmt;

#[derive(Debug)]
struct MinMax(i64, i64);

// Реализуем `Display` для `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "({}, {})", self.0, self.1)
    }
}

#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// По аналогии, реализуем `Display` для Point2D
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Обращаться к полям структуры Point2D будет по имени
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("Большой диапазон - {big} и маленький диапазон {small}",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Display: {}", point);
    println!("Debug: {:?}", point);
}
```

```rust
use std::fmt;

// Определяем структуру с именем `List`, которая хранит в себе `Vec`.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        let vec = &self.0;

        write!(f, "[")?;

        for (count, v) in vec.iter().enumerate() {
            // Для каждого элемента, кроме первого, добавим запятую
            // до вызова `write!`. Используем оператор `?` или `try!`,
            // чтобы вернуться при наличии ошибок.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // Закроем открытую скобку и вернём значение `fmt::Result`
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```
