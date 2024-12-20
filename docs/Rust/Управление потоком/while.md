
*Теги*: [[Rust]], [[Управление потоком]]

```rust
fn main() {
    let mut n = 1;

    // Цикл while будет работать, пока `n` меньше 101
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // Увеличиваем значение счётчика
        n += 1;
    }
}
```

## while let

```rust
fn main() {
    // Создадим переменную `optional` с типом `Option<i32>`
    let mut optional = Some(0);

    // Это можно прочитать так: "Пока `let` деструктурирует `optional` в
    // `Some(i)`, выполняем блок (`{}`). В противном случае `break`.
    while let Some(i) = optional {
        if i > 9 {
            println!("Больше 9, уходим отсюда!");
            optional = None;
        } else {
            println!("`i` равен `{:?}`. Попробуем ещё раз.", i);
            optional = Some(i + 1);
        }
    }
    // ^ К `if let` можно добавить дополнительный блок `else`/`else if`
    // Для `while let` подобного нет.
}
```
