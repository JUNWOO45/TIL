# Types



## Array

- 배열의 타입은 두가지 방법 중 하나로 작성될 수 있습니다.

```typescript
const list: number[] = [1, 2, 3];

const list2: Array<number> = [1, 2, 3];
```



## Tuple

- 고정된 개수의 요소 타입을 알고있지만, 반드시 같을 필요는 없는 배열을 표현합니다.

```typescript
let x: [string, number];

x = ['hello', 10];

x= [10, 'hello'];	// Error
```



## Any

- 알지 못하는 변수의 타입

```typescript
let notSure: any = 4;
notSure = '문자열이 될 수 있음.';
notSure = false;
```



## Void

- 일반적으로 return 값을 반환하지 않는 함수의 반환 타입으로 볼 수 있습니다.

```typescript
function test: void {
  console.log('hi');
}
```

- void 타입의 변수선언은 `undefined` 또는 `null` 만 할당할 수 있습니다.

```typescript
const unusable: void = undefined;
```

