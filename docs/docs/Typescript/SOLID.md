# Принципы S.O.L.I.D.

Теги: [[Typescript/README]], [[docs/Typescript/SOLID]]

- [[#Single responsibility principle]]
- [[#Open/closed principle]]
- [[#Liskov substitution principle]]
- [[#Interface segregation principle]]
- [[#Dependency inversion principle]]

## Single responsibility principle

**Принцип единственной обязанности** - одна конкретная сущность решает одну задачу.
 
👎**Bad:**
```typescript
class Auto {
	constructor(model: string) {}
	getCarModel() {}
	setCarModel() {}
	saveCustomerOrder(order: Auto) {}
	getCustomerOrder(id: string) {}
	removeCustomerOrder(id: string) {}
	updateCarSet(set: object) {}
}
```

👍**Good:**
```typescript
class Auto {
	constructor(model: string) {}
	getCarModel() {}
	setCarModel() {}
}

class CustomerAuto {
	saveCustomerOrder(order: Auto) {}
	getCustomerOrder(id: string) {}
	removeCustomerOrder(id: string) {}
}

class AutoDB {
	updateCarSet(set: object) {}
}
```

## Open/closed principle

**Принцип открытости/закрытости**

👎**Bad:**
```typescript
class Auto {
	constructor(public model: string) {}
	getCarModel() {}
}

const shop: Array<Auto> = [
	new Auto('Tesla'),
	new Auto('Audi'),
	new Auto('BMW')
]

const getPrice = (auto: Array<Auto>): string | void => {
	for (let i = 0; i < auto.length; i++) {
		switch (auto[i].model) {
			case 'Tesla': return '80 000$'
			case 'Audi': return '50 000$'
			case 'BMW': return '70 000$'
			default: return 'No Auto Price'
		}
	}
}

getPrice(shop)
```

👍**Good:**
```typescript
abstract class CarPrice {
	abstract getPrice(): string
}

class Tesla extends CarPrice {
	getPrice() {
		return '80 000$'
	}
}

class Audi extends CarPrice {
	getPrice() {
		return '50 000$'
	}
}

class Bmw extends CarPrice {
	getPrice() {
		return '70 000$'
	}
}

const shop: Array<CarPrice> = [
	new Tesla(),
	new Audi(),
	new Bmw()
]

const getPrice = (auto: Array<CarPrice>): string | void => {
	for (let i = 0; i < auto.length; i++) {
		auto[i].getPrice()
	}
}

getPrice(shop)
```

## Liskov substitution principle

**Принцип подстановки Лисков**

👎**Bad:**
```typescript
class Rectangle {
	constructor(public width: number, public height: number) {}
	
	setWidth(width: number) {
		this.width = width
	}
	
	setHeight(height: number) {
		this.height = height
	}
	
	areaOf(): number {
		return this.width * this.height
	}
}

class Square extends Rectangle {
	width: number = 0
	height: number = 0
	
	constructor(size: number) {
		super(size, size)
	}
	
	setWidth(width: number) {
		this.width = width
		this.height = width
	}
	
	setHeight(height: number) {
		this.width = height
		this.height = height
	}
}
```

👍**Good:**
```typescript
interface Figure {
	setWidth(width: number): void
	setHeight(height: number): void
	areaOf(): void
}

class Rectangle implements Figure {
	setWidth(width: number) {}
	setHeight(height: number) {}
	areaOf() {}
}

class Square implements Figure {
	setWidth(width: number) {}
	setHeight(height: number) {}
	areaOf() {}
}
```

## Interface segregation principle

**Принцип разделения интерфейсов**

👎**Bad:**
```typescript
interface AutoSet {
	getTeslaSet(): any
	getAudiSet(): any
	getBmwSet(): any
}

class Tesla implements AutoSet {
	getTeslaSet(): any {}
	getAudiSet(): any {}
	getBmwSet(): any {}
}

class Audi implements AutoSet {
	getTeslaSet(): any {}
	getAudiSet(): any {}
	getBmwSet(): any {}
}

class Bmw implements AutoSet {
	getTeslaSet(): any {}
	getAudiSet(): any {}
	getBmwSet(): any {}
}
```

👍**Good:**
```typescript
interface TeslaSet {
	getTeslaSet(): any
}

interface AudiSet {
	getAudiSet(): any
}

interface BmwSet {
	getBmwSet(): any
}

class Tesla implements TeslaSet {
	getTeslaSet(): any {}
}

class Audi implements AudiSet {
	getAudiSet(): any {}
}

class Bmw implements BmwSet {
	getBmwSet(): any {}
}
```

## Dependency inversion principle

**Принцип инверсии зависимостей**

👎**Bad:**
```typescript
class xmlHttpRequestService {}

// Low level
class xmlHttpService extends xmlHttpRequestService {
	request(url: string, type: string) {}
}

// High level module
class Http {
	constructor(private xmlHttpService: xmlHttpService) {}
	
	get(url: string, options: any) {
		this.xmlHttpService.request(url, 'GET')
	}
	
	post(url: string) {
		this.xmlHttpService.request(url, 'POST')
	}
}
```

👍**Good:**
```typescript
class xmlHttpRequestService {
	open() {}
	send() {}
}

interface Connection {
	request(url: string, options: any): any
}

// Low level
class xmlHttpService implements Connection {
	xhr = new xmlHttpRequestService()
	
	request(url: string, type: string) {
		this.xhr.open()
		this.xhr.send()
	}
}

// High level module
class Http {
	constructor(private httpConnection: Connection) {}
	
	get(url: string, options: any) {
		this.httpConnection.request(url, 'GET')
	}
	
	post(url: string) {
		this.httpConnection.request(url, 'POST')
	}
}
```

Источник: [Просто о SOLID (Принципы SOLID)](https://youtu.be/A6wEkG4B38E)
