# Debug

*Теги*: [[Rust]], [[Форматированный вывод]]

```rust
#[derive(Debug)]
struct Structure(i32);

#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // Вывод с помощью `{:?}` аналогичен `{}`.
    println!("{:?} месяцев в году.", 12);
    println!("{1:?} {0:?} - это имя {actor:?}.",
             "Слэйтер",
             "Кристиан",
             actor="актёра");

    println!("Теперь {:?} будет выведена на экран!", Structure(3));

    // Проблема с выводом `derive`, в том, что у нас не будет контроля
    // над тем, как будет выглядеть результат.
    // Что, если мы хотим напечатать просто `7`?
    println!("А теперь напечатаем {:?}", Deep(Structure(7)));
}
```

Rust также обеспечивает "красивую печать" с помощью `{:#?}`.

```rust
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // Pretty print
    println!("{:#?}", peter);
}
```

```rust

```

```rust

```
