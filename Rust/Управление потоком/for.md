
*Теги*: [[Rust]], [[Управление потоком]]

```rust
fn main() {
    // `n` будет принимать значения: 1, 2, ..., 100 с каждой итерации
    // for n in 1..=100 {
    // или
    for n in 1..101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

## Итераторы

- `iter` - эта функция заимствует каждый элемент коллекции на каждой итерации. Благодаря этому, он оставляет коллекцию нетронутой и доступной для использования после цикла.
- `into_iter` - эта функция потребляет коллекцию так что на каждой итерации предоставляются данные. Коллекция больше не доступна для использования так как владение ею перешло в эту функцию.
- `iter_mut` - эта функция делает изменяемое заимствование каждого элемента коллекции, позволяя изменять коллекцию на месте.

```rust
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter() {
        match name {
            &"Ferris" => println!("Программисты Rust вокруг нас!"),
            _ => println!("Привет {}", name),
        }
    }
}
```

```rust
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.into_iter() {
        match name {
            "Ferris" => println!("Программисты Rust вокруг нас!"),
            _ => println!("Привет {}", name),
        }
    }
}
```

```rust
fn main() {
    let mut names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter_mut() {
        *name = match name {
            &mut "Ferris" => "Программисты Rust вокруг нас!",
            _ => "Привет",
        }
    }

    println!("имена: {:?}", names);
}
```
