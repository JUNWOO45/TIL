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





## Reference

- [https://www.typescriptlang.org/docs/handbook/classes.html](https://www.typescriptlang.org/docs/handbook/classes.html)