# Форматированный вывод

*Теги*: [[Rust]]

```rust
fn main() {
    // `{}` автоматически будет заменено на
    // аргументы. Они будут преобразованы в строку.
    println!("{} дней", 31);

    // Без суффиксов, 31 является i32.
    // Можно изменить тип 31, используя суффикс.

    // Существует множество способов работы с форматированным выводом.
    // Можно указать позицию для каждого аргумента.
    println!("{0}, это {1}. {1}, это {0}", "Алиса", "Боб");

    // Так же можно именовать аргументы.
    println!("{subject} {verb} {object}",
             object="ленивую собаку",
             subject="быстрая коричневая лиса",
             verb="прыгает через");

    println!("{} из {:b} людей знают, что такое двоичный код.", 1, 2);

    // Можно выравнивать текст, сдвигая его на указанную ширину.
    // Данный макрос отобразит в консоли
    // "     1". 5 пробелов и "1".
    println!("{number:>width$}", number=1, width=6);

    // Можно добавить к цифрам пару нулей. Данный макрос выведет "000001".
    println!("{number:0>width$}", number=1, width=6);
}
```

| Трейт               | Маркер | Описание                                                              |
|---------------------|--------|-----------------------------------------------------------------------|
| `std::fmt::Debug`   | `{:?}` | Форматирует текст для отладочных целей.                               |
| `std::fmt::Display` | `{}`   | Форматирует текст в более элегантном, удобном для пользователя стиле. |

## Особенности форматирования

| Маркер  | Трейт                                                                                                 | Пример                                                   |
|---------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
|         |                                                                                                       | `let x = 42;`                                            |
| `{}`    | [`Display`](https://doc.rust-lang.org/std/fmt/trait.Display.html "характеристика std::fmt:: Дисплей") | `assert_eq!(format!("{}", x), "42");`                    |
| `{:?}`  | [`Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html "черта std::fmt::Debug")                 |                                                          |
| `{:#?}` | [`Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html "черта std::fmt::Debug")                 |                                                          |
| `{:x?}` | [`Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html "черта std::fmt::Debug")                 | *с шестнадцатеричными целыми числами в нижнем регистре*  |
| `{:X?}` | [`Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html "черта std::fmt::Debug")                 | *с шестнадцатеричными целыми числами в верхнем регистре* |
| `{:o}`  | [`Octal`](https://doc.rust-lang.org/std/fmt/trait.Octal.html "признак std::fmt:: Восьмеричный")       | `assert_eq!(format!("{x:o}"), "52");`                    |
| `{:#o}` | [`Octal`](https://doc.rust-lang.org/std/fmt/trait.Octal.html "признак std::fmt:: Восьмеричный")       | `assert_eq!(format!("{x:#o}"), "0o52");`                 |
| `{:x}`  | [`LowerHex`](https://doc.rust-lang.org/std/fmt/trait.LowerHex.html "признак std::fmt::LowerHex")      | `assert_eq!(format!("{y:x}"), "2a");`                    |
| `{:#x}` | [`LowerHex`](https://doc.rust-lang.org/std/fmt/trait.LowerHex.html "признак std::fmt::LowerHex")      | `assert_eq!(format!("{y:#x}"), "0x2a");`                 |
| `{:X}`  | [`UpperHex`](https://doc.rust-lang.org/std/fmt/trait.UpperHex.html "признак std::fmt:: UpperHex")     | `assert_eq!(format!("{y:X}"), "2A");`                    |
| `{:#X}` | [`UpperHex`](https://doc.rust-lang.org/std/fmt/trait.UpperHex.html "признак std::fmt:: UpperHex")     | `assert_eq!(format!("{y:#X}"), "0x2A")`                  |
| `{:p}`  | [`Pointer`](https://doc.rust-lang.org/std/fmt/trait.Pointer.html "признак std::fmt::Указатель")       | `let address = format!("{&x:p}"); // '0x7f06092ac6d0'`   |
| `{:b}`  | [`Binary`](https://doc.rust-lang.org/std/fmt/trait.Binary.html "признак std::fmt::Двоичный")          | `assert_eq!(format!("{x:b}"), "101010");`                |
| `{:#b}` | [`Binary`](https://doc.rust-lang.org/std/fmt/trait.Binary.html "признак std::fmt::Двоичный")          | `assert_eq!(format!("{x:#b}"), "0b101010");`             |
| `{:e}`  | [`LowerExp`](https://doc.rust-lang.org/std/fmt/trait.LowerExp.html "признак std::fmt::LowerExp")      | `assert_eq!(format!("{x:e}"), "4.2e1");`                 |
| `{:E}`  | [`UpperExp`](https://doc.rust-lang.org/std/fmt/trait.UpperExp.html "признак std::fmt::UpperExp")      | `assert_eq!(format!("{x:E}"), "4.2E1");`                 |

## Форматирование

```rust
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // Широта
    lat: f32,
    // Долгота
    lon: f32,
}

impl Display for City {
    // `f` — это буфер, данный метод должен записать в него форматированную строку
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!` похож на `format!`, только он запишет форматированную строку
        // в буфер (первый аргумент функции)
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

fn main() {
    for city in [
        City { name: "Дублин", lat: 53.347778, lon: -6.259722 },
        City { name: "Осло", lat: 59.95, lon: 10.75 },
        City { name: "Ванкувер", lat: 49.25, lon: -123.1 },
    ].iter() {
        println!("{}", *city);
    }
}
```

```rust

```