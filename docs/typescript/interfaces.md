# Interfaces

---

## Basic



```typescript
function printLabel(obj: { label: string }) {
  console.log(obj.label);
}

const myObj = {
  size: 100,
  label: 'hello world'
};

printLabel(myObj);	// 'hello world'
```



printLabel함수에는 객체를 전달하는 단일 매개변수가 존재하며, 이 매개변수는 string 타입의 label 프로퍼티를 가집니다.

실제로 넘겨지는 myObj를 확인하면, string 타입의 label 프로퍼티 이 외에도 number 타입의 size 프로퍼티도 존재합니다.

하지만, 컴파일러는 필요한 속성이 `최소한 존재` 하고, `타입과 일치` 하는지만 확인합니다.



인터페이스를 사용하여 다음과같이 작성할 수 있습니다.

```typescript
interface LabelledValue {
  label: string;
}

function printLabel(obj: LabelledValue) {
  console.log(obj.label);
}

const myObj = {
  size: 100,
  label: 'hello world'
};

printLabel(myObj);	// 'hello world'
```



---

## Optional Properties

> 처음엔 이해를 못하고 많이 검색해봤는데 굉장히 간단한 내용이었다.

인터페이스의 프로퍼티는 반드시 구현되어야한다.

하지만 인터페이스의 프로퍼티가 선택적으로 필요한 경우, 프로퍼티명 뒤에 `?` 를 붙이면 프로퍼티가 없더라도 에러가 발생하지 않는다.



```typescript
interface TestInterface {
    name: string;
    age: number;
    address: string;
    food: string;
}

function printObj(obj: TestInterface) {
    console.log('obj : ', obj);
}

const targetObj = {
    name: 'junwoo',
    age: 100,
    address: 'dongtan'
};

printObj(targetObj);
// Property 'food' is missing in type '{ name: string; age: number; address: string; }' but required in type 'TestInterface'.
```

이렇게 에러가 발생하는 것을,

```typescript
interface TestInterface {
    name: string;
    age: number;
    address: string;
    food?: string;
}

function printObj(obj: TestInterface) {
    console.log('obj : ', obj);
}

const targetObj = {
    name: 'junwoo',
    age: 100,
    address: 'dongtan'
};

printObj(targetObj);
```



정말 편하다.

---

## Readonly Properties

```types
interface Point {
    readonly x: number;
    readonly y: number;
}

let p1: Point = { x: 10, y: 20 };
p1.x = 5;
// Cannot assign to 'x' because it is a read-only property.
```

할당 후, x와 y는 바꿀 수 없습니다.



## 함수 인터페이스

함수 또한 인터페이스로 정의가능하다.

```typescript
interface SumFunc {
  (a: number, b: number): number;
}

const sum: SumFunc = (a: number, b: number): number => a + b;
```





## Types와 뭐가 다른거야?

- types는 확장 불가능/ interface 는 확장 가능
- 그러면 types는 왜 있는 걸까🤔..
  - 참고: https://joshua1988.github.io/ts/guide/type-alias.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD-type-aliases



---

## References

- https://www.typescriptlang.org/docs/handbook/interfaces.html
- https://typescript-kr.github.io/pages/Interfaces.html
- https://poiemaweb.com/typescript-interface

