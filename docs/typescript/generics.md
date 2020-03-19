# Generic

```typescript
function identity(arg: string): string {
  return arg;
}
```

`any` 를 사용해보이면 모든 타입을 전달받을 수 있지만, 함수가 반환될 때 그 타입이 무엇이었는지에 대한 정보를 잃어버리게된다.

```typescript
function identity(arg: any): any {
  return arg;
}
```

그래서,

제네릭이란게 있다.

```typescript
function identity<T>(arg: T): T {
  return arg;
}
```

이렇게 만든 함수는, 두가지 방법 중 하나로 호출할 수 있다.

- 모든 인수를 함수에 전달하는 방법

```typescript
let result = identity<string>("hello");
```

명시적으로 `T` 를 `string` 타입로 정했다.

- 타입 인수 추론(type argument inference) 를 사용하는 방법

  함수에 전달하는 인수 타입에 따라 컴파일러가 자동으로 `T` 를 설정하는 방법이다.

```typescript
let result = identity("hello");
```

꺾쇠 안에 명시적으로 타입을 전달할 필요가 없다.

더 일반적인 방법이라고할 수 있겠다.

<br>

`length` 메소드를 사용하고싶다고 해보자.

```typescript
function identity<T>(arg: T): T {
	console.log(arg.length);
  return arg;
}
```

`string` 타입이나 `배열` 같은 경우, `length` 메소드를 사용할 수 있지만 `number` 타입의 경우엔 `length` 메소드가 없으므로 에러를 발생시키게된다.

```typescript
function identity<T>(arg: T[]): T[] {
  console.log(arg.length);
  
  return arg;
}

identity([1, 2, 3]);	// 3
identity('abc');	// Argument of type '"123"' is not assignable to parameter of type 'unknown[]'.

identity(['abc']);	// 1
```

identity 함수는 타입 매개 변수 `T` 를 인수로 받고, `arg` 는 `T` 배열이며 `T` 배열을 반환한다.

이렇게 작성할 수도 있다.

```typescript
function identity<T>(arg: Array<T>): Array<T> {
  console.log(arg.length);
  
  return arg;
}
```

