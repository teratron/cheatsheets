# Принципы S.O.L.I.D.

Теги: [[Rust]], [[Rust/SOLID]]

- [[#Принцип единой ответственности (SRP)]]
- [[#Принцип "Открыто-закрыто" (OCP)]]
- [[#Принцип замены Лисков (LSP)]]
- [[#Принцип разделения интерфейса (ISP)]]
- [[#Принцип инверсии зависимостей (DIP)]]

## Принцип единой ответственности (SRP)

**Принцип единой ответственности** гласит, что модуль, класс или функция должны нести единую ответственность. Он должен
отвечать за одну и только одну часть общей функциональности. Применение SRP помогает улучшить ремонтопригодность и
читабельность кода.

В Rust вы можете придерживаться SRP, следя за тем, чтобы каждый модуль или структура имели четкое и целенаправленное
назначение. Например, рассмотрим простую реализацию модуля обработки файлов:

```rust
pub mod file_utils {
    pub fn read_file(path: &str) -> String {
        // Read file implementation
    }
	
    pub fn write_file(path: &str, content: &str) {
        // Write file implementation
    }
}
```

В этом примере `file_utils` модуль имеет отдельные функции для чтения и записи файлов, каждая из которых выполняет
отдельную ответственность. Сохраняя сфокусированность функций, становится проще понимать кодовую базу и поддерживать ее.

## Принцип "Открыто-закрыто" (OCP)

**Принцип "Открыто-закрыто"** предполагает, что модули, классы или функции должны быть открыты для расширения, но
закрыты для модификации. В нем делается упор на разработку кода таким образом, чтобы новые функции могли быть добавлены
без изменения существующего кода. Это способствует повторному использованию кода и сводит к минимуму риск появления
ошибок.

В Rust вы можете следовать OCP, используя признаки и реализуя их для разных типов. Рассмотрим пример, где у нас есть
модуль shape, который определяет признак под названием `Shape`:

```rust
pub trait Shape {
    fn area(&self) -> f64;
}

pub struct Circle {
    radius: f64,
}

impl Shape for Circle {
    fn area(&self) -> f64 {
        // Calculate circle area implementation
    }
}

pub struct Rectangle {
    width: f64,
    height: f64,
}

impl Shape for Rectangle {
    fn area(&self) -> f64 {
        // Calculate rectangle area implementation
    }
}
```

Определяя `Shape` признак, мы создаем открытую систему, в которой можно добавлять новые формы путем реализации `Shape`
признаков без изменения существующего кода. Это обеспечивает легкую расширяемость и способствует повторному
использованию кода.

## Принцип замены Лисков (LSP)

**Принцип подстановки Лисков** гласит, что объекты суперкласса должны заменяться объектами его подклассов без ущерба для
корректности программы. Другими словами, производные типы должны иметь возможность беспрепятственно заменять свои
базовые типы.

В Rust LSP может быть обеспечен тщательным проектированием иерархий наследования и соблюдением поведения базовых типов.
Например, рассмотрим сценарий, в котором у нас есть `Bird` базовая структура и `Duck` структура, которая наследуется от
нее:

```rust
pub struct Bird {
    pub fn fly(&self) {
        // Fly implementation
    }
}

pub struct Duck {
    bird: Bird,
}

impl Duck {
    pub fn new() -> Self {
        Duck { bird: Bird::new() }
    }
	
    pub fn fly(&self) {
        self.bird.fly();
    }
	
    pub fn quack(&self) {
        // Quack implementation
    }
}
```

В этом примере `Duck` структура наследуется от `Bird` struct , но это не изменяет поведение `fly` метода. Это
соответствует LSP, позволяя использовать `Duck` инстанс взаимозаменяемо с `Bird` инстансом.

## Принцип разделения интерфейса (ISP)

**Принцип разделения интерфейсов** рекомендует, чтобы клиенты не были вынуждены зависеть от интерфейсов, которые они не
используют. Он продвигает идею небольших, ориентированных интерфейсов, а не больших, монолитных. Это помогает снизить
нагрузку и гарантирует, что клиенты зависят только от необходимых им функциональных возможностей.

В Rust вы можете следовать примеру провайдера, создавая функции с минимальной и целостной функциональностью. Например,
рассмотрим систему обмена сообщениями с двумя типами сообщений: электронной почтой и SMS:

```rust
pub trait Email {
    fn send_email(&self);
}

pub trait SMS {
    fn send_sms(&self);
}

pub struct NotificationSystem<T: Email + SMS> {
    transport: T,
}

impl<T: Email + SMS> NotificationSystem<T> {
    pub fn new(transport: T) -> Self {
        NotificationSystem { transport }
    }
	
    pub fn send_notification(&self) {
        self.transport.send_email();
        self.transport.send_sms();
    }
}
```

В этом примере определены отдельные функции для функций электронной почты и SMS, что позволяет клиентам полагаться
только на требуемые функции. Это гарантирует, что клиенты не будут перегружены ненужными им функциональными
возможностями, способствуя созданию более гибкой и поддерживаемой кодовой базы.

## Принцип инверсии зависимостей (DIP)

**Принцип инверсии зависимостей** предполагает, что модули высокого уровня не должны зависеть от модулей низкого уровня.
Вместо этого оба должны зависеть от абстракций. Это способствует ослаблению связи и обеспечивает гибкость при выборе
различных реализаций, не затрагивая модули более высокого уровня.

В Rust вы можете следовать DIP, используя черты в качестве абстракций и полагаясь на эти абстракции, а не на конкретные
реализации. Рассмотрим пример, где у нас есть модуль ведения журнала.:

```rust
pub trait Logger {
    fn log(&self, message: &str);
}

pub struct Application {
    logger: Box<dyn Logger>,
}

impl Application {
    pub fn new(logger: Box<dyn Logger>) -> Self {
        Application { logger }
    }
	
    pub fn run(&self) {
        self.logger.log("Application started");
        // Application logic
        self.logger.log("Application ended");
    }
}
```

В этом примере `Application` структура зависит от `Logger` признака, а не от конкретной реализации. Это позволяет
предоставлять различные реализации регистратора во время выполнения без изменения `Application` кода. Разделение,
достигаемое за счет погружения, повышает гибкость и тестируемость.
