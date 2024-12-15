
*Теги*: [[Rust]], [[Управление потоком]]

```rust
fn main() {
    let mut count = 0u32;

    // Бесконечный цикл
    loop {
        count += 1;

        if count == 3 {
            println!("три");

            // Пропустить оставшуюся часть цикла
            continue;
        }

        println!("{}", count);

        if count == 5 {
            println!("Всё, достаточно");

            // Выйти из цикла
            break;
        }
    }
}
```

## Вложенность и метки

```rust
#![allow(unreachable_code)]

fn main() {
    'outer: loop {
        println!("Вошли во внешний цикл");

        'inner: loop {
            println!("Вошли во внутренний цикл");

            // Это прервёт лишь внутренний цикл
            //break;

            // Это прервёт внешний цикл
            break 'outer;
        }

        println!("Эта точка не будет достигнута");
    }

    println!("Вышли из внешнего цикла");
}
```

## Возврат из циклов

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    assert_eq!(result, 20);
}
```

```rust

```

```rust

```
