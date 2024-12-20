# Объектно-ориентированное программирование

---

## Парадигмы ООП

- [[#Объект]]
- [[#Класс]]
- [[#Экземпляр]]
- [[#Наследование]]
- [[#Инкапсуляция]]
- [[#Полиморфизм]]
- [[#Интерфейс]]
- [[#Абстракция]]
- [[#Композиция]]
- [[#Агрегация]]

## Объект

```typescript
const bmwAuto = {
	name: 'BMW',
	model: 'X6',
	year: 2024,
	
	getAutoType() {
		return `${this.name} ${this.model} - ${this.year}`
	}
}
```

## Класс

```typescript
class Auto {
	constructor(name, model, year) {
		this.name = name
		this.model = model
		this.year = year
	}
	
	getAutoType() {
		return `${this.name} ${this.model} - ${this.year}`
	}
}
```

## Экземпляр класса (Instance)

```typescript
// Instance creation
const bmwAuto = new Auto('BMW', 'X6', 2024)
const audiAuto = new Auto('Audi', 'Q7', 2020)
const teslaAuto = new Auto('Tesla', '3', 2019)

bmwAuto.getAutoType()    // BMW X6 - 2024
audiAuto.getAutoType()   // Audi Q7 - 2020
teslaAuto.getAutoType()  // Tesla 3 - 2019
```

## Наследование

**Наследование в объектно-ориентированном программировании** — это концепция, согласно которой одни классы, называемые родительскими, могут лежать в основе других — дочерних. При этом, дочерние классы перенимают свойства и поведение своего родителя.

```typescript
class TeslaCar extends Auto {
	constructor(name, model, year) {
		super(name, model, year)
		this.name = name
		this.model = '${model} Model'
		this.year = year
	}
	
	getCarModel() {
		return this.model
	}
}

// Instance creation
const teslaAuto = new TeslaCar('Tesla', '3', 2019)

// Own method
teslaAuto.getCarModel()  // 3 Model

// Inherited method
teslaAuto.getAutoType()  // Tesla 3 - 2019
```

## Инкапсуляция

**Инкапсуляция** _(от лат. in capsule — в оболочке)_ — это заключение данных и функциональности в оболочку. В ООП в роли оболочки выступают классы: они не только собирают переменные и методы в одном месте, но и защищают их от вмешательства извне _(сокрытие)_.

```typescript
class Auto {
	public name: string
	public model: string
	public year: number
	private vin: number
	
	constructor(name: string, model: string, year: number) {
		this.name = name
		this.model = model
		this.year = year
		this.vin = new Date().getTime()
	}
	
	get vinNumber() {
		return this.vin
	}
}

const audiAuto = new Auto('Audi', 'Q7', 2020)

audiAuto.name      // Audi
audiAuto.model     // Q7
audiAuto.vin       // Property 'vin' is private...
audiAuto.vinNumber // 1635164984459
```

## Полиморфизм

**Полиморфизм** даёт возможность использовать одни и те же методы для объектов разных классов.

```typescript
class BmwCar extends Auto {
	getAutoType() {
		return `${this.year}, ${this.name}, ${this.model}`
	}
}

class AudiCar extends Auto {
	getAutoType() {
		return `${this.year}, ${this.name} ${this.model}`
	}
}

class TeslaCar extends Auto {
	getAutoType() {
		return `${this.name} ${this.model} / ${this.year}`
	}
}

const bmwAuto = new BmwCart('BMW', 'X6', 2024)
const audiAuto = new AudiCart('Audi', 'Q7', 2020)
const teslaAuto = new TeslaCar('Tesla', '3', 2019)

const getAutoTypes = autos => autos.map(auto => auto.getAutoType())

const autoTypes = getAutoTypes([bmwAuto, audiAuto, teslaAuto])
// ['2024, BMW, X6', '2020, Audi Q7', 'Tesla 3 / 2019']
```

## Интерфейс

```typescript
interface AutoFactory {
	readonly name: string
	readonly model: string
	year: number
	
	getAutoType(): string
}

class Auto implements AutoFactory {
	public name: string
	public model: string
	public year: number
	
	constructor(name: string, model: string, year: number) {
		this.name = name
		this.model = model
		this.year = year
	}
	
	getAutoType() {
		return `${this.name} ${this.model} / ${this.year}`
	}
}
```

## Абстракция

```typescript
abstract class AutoFactory {
	readonly name: string
	readonly model: string
	year: number
	
	abstract getAutoType(): string
	
	getAutoModel(): string {
		return this.model
	}
}

class Auto extends AutoFactory {
	public name: string
	public model: string
	public year: number
	
	constructor(name: string, model: string, year: number) {
		super()
		this.name = name
		this.model = model
		this.year = year
	}
	
	getAutoType() {
		return `${this.name} ${this.model} / ${this.year}`
	}
}

const bmwAuto = new Auto('BMW', 'X6', 2024)

// Own method
bmwAuto.getAutoType()   // BMW X6 / 2024

// Inherited from abstract class method
bmwAuto.getAutoModel()  // X6
```

## Композиция

```typescript
class Engine {
	start() {
		return 'Engine is started'
	}
}

class Wiring {
	start() {
		return 'Wiring is started'
	}
}

class FuelPump {
	start() {
		return 'FuelPump is started'
	}
}

class Car {
	constructor() {
		// Composition
		this.engine = new Engine()
		this.wiring = new Wiring()
		this.fuelPump = new FuelPump()
	}
	
	start() {
		this.engine.start()
		this.wiring.start()
		this.fuelPump.start()
	}
}
```

## Агрегация

```typescript
class Autopilot {
	navigate() {
		return 'Navigation is started'
	}
}

class Car {
	constructor(autopilot) {
		this.engine = new Engine()
		this.wiring = new Wiring()
		this.fuelPump = new FuelPump()
		this.autopilot = autopilot
	}
	
	start() {
		this.engine.start()
		this.wiring.start()
		this.fuelPump.start()
	}
}

const bmwAuto = new Car(new Autopilot())
bmwAuto.start()
bmwAuto.autopilot.navigate()

class Airplane {
	constructor(autopilot) {
		this.autopilot = autopilot
	}
}

const boeing = new Airplane(new Autopilot())

class Helicopter {
	constructor(autopilot) {
		this.autopilot = autopilot
	}
}

const mi8 = new Helicopter(new Autopilot())
```

---

Источник: [Просто о ООП (Парадигмы ООП)](https://www.youtube.com/watch?v=VjGdjqyXbhg)

Теги: [[Typescript/README]], [[oop]]