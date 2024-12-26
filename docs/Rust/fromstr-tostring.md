# FromStr и ToString

*Теги*: [[Rust]], [[Преобразования]]

## Конвертация в строку

Преобразовать любой тип в `String` так же просто, как и реализовать для него типаж `ToString`. Вместо того, чтобы делать
это напрямую, вы должны реализовать типаж `fmt::Display`, который автоматически предоставляет реализацию `ToString`.

```rust
use std::fmt;

struct Circle {
    radius: i32
}

impl fmt::Display for Circle {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Круг радиусом {}", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```

## Парсинг строки

Это преобразует строку в указанный тип при условии, что для этого типа реализован типаж `FromStr`.

```rust
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let sum = parsed + turbo_parsed;
    println!("Сумма: {:?}", sum);
}
```
