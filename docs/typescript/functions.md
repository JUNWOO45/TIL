# Functions



- 각 매개변수에 타입을 추가 한 다음, 함수 자체에도 타입을 추가하여 반환 타입을 추가할 수 있습니다.

```typescript
function add(x: number, y: nunber): number {
  return x + y;
}
```



---



## Optional and Default Parameters



### Optional Parameters

- 타입스크립트에서는 모든 매개변수가 함수에 필요하다고 가정합니다.
  - 자바스크립트에서는 모든 매개변수는 선택사항이며, 매개변수가 없을 경우 undefined로 처리합니다.

```typescript
function buildName(firstName: string, lastName: string) {
  return `${firstName} ${lastName}`;
}

const result1 = buildName('park');
//Expected 2 arguments, but got 1.

const result2 = buildName('park', 'junwoo', 'paul');
//Expected 2 arguments, but got 3
```



- 타입스크립트에서 선택적 매개변수(Optional Parameters) 를 사용하려면, 매개변수의 끝에 `?` 를 추가해야합니다.

```typescript
function buildName(firstName: string, lastName?: string) {
  if(lastName) {
    return `${fistName} ${lastName}`;
  }
  
  return firstName;
}
```



### Default Parameters

```typescript
function buildName(firstName: string, lastName:string = 'junwoo') {
  return `${firstName} ${lastName}`;
}


buildName('park');	//'park junwoo'
buildName('park', 'haha');	//'park haha'
```



---

## Rest Parameters

```typescript
function buildName(firstName: string, ...restName: string[]) {
  return `${firstName} ${restName.join(' ')}`;
}

buildName('park', 'abc', 'def', 'ggg');
//'park abc def ggg'
```



