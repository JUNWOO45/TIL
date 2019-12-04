# Classes

```typescript
class Animal {
  move(distance: number = 0) {
    console.log(`Animal moved ${distance}m.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof!!');
  }
}

const dog = new Dog();
dog.bark();
dog.move(15);
```

`extends` : extends키워드를 상속하여 Animal 클래스를 상속받을 수 있습니다.

이러한 Animal 클래스를 `superclasses` , Dog 클래스를 `subclasses` 라고 부릅니다.



```typescript
class Animal {
  name: string;
  constructor(theName: string) {
    this.name = theName;
  }
  
  move(distance: number = 0) {
    console.log(`${this.name} moved ${distance}m.`);
  }
}

class Snake extends Animal {
  constructor(name: string) {
    super(name);
  }
  
  move(distance:number = 5) {
    console.log('뱀뱀..');
    super.move(distance);
  }
}

class Horse extends Animal {
  constructor(name: string) {
    super(name);
  }
  
  move(distance:number = 100) {
    console.log('말말..');
    super.move(distance);
  }
}

const sam = new Snake('junwoo');
sam.move(123);

const tom: Animal = new Horse('말말');
tom.move();
```



생성자 함수를 포함하는 각 subclasses는 superclasses의 생성자를 실행할 `super()` 를 호출해야 합니다.

> 아하... super()는 superclasses의 생성자함수(constructor)를 실행하는 거구나.

또한, subclasses의 메소드는 superclasses의 메소드를 오버라이드할 수 있습니다.



---

### public, private, protected modifiers(지정자)

- 명시하지않으면 기본적으로 public.
- private 이해하기
  - 멤버가 `private` 으로 표시되어있으면, 그 멤버를 포함하는 클래스의 외부에서는 접근할 수 없습니다.

```type
class Animal {
	private name: string;
	constructor(name: string) {
		this.name = name;
	}
}

new Animal('cat').name;
// Property 'name' is private and only accessible within class 'Animal'.
```



- protected 이해하기
  - `protected` 멤버는 선언된 subclasses의 인스턴스에서 접근할 수 있습니다.

```type
class Person {
    protected name: string;
    constructor(name: string) {
        this.name = name;
    }
}

class Employee extends Person {
    private department: string;

    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }

    public say() {
        return `Hello, my name is ${this.name} AND work in ${this.department}`;
    }
}

const newbie = new Employee('junwoo', 'development');

console.log(newbie.say()); //Hello, my name is junwoo AND work in development
console.log(newbie.name);	
// Property 'name' is protected and only accessible within class 'Person' and its subclasses

```



- Readonly modifier

```types
class Octopus {
	readonly name: string;
	readonly legs: number = 8;
	
	constructor(name: string) {
		this.name = name;
	}
}

const target1 = new Octopus('IAMOCT1');
target1.name = 'hihi';
// Cannot assign to 'name' because it is a read-only property
```





## Reference

- [https://www.typescriptlang.org/docs/handbook/classes.html](https://www.typescriptlang.org/docs/handbook/classes.html)