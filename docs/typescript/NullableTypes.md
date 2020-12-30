

## Non-Nullable Types

### Example

`null`과 `undefined` 모두 string타입변수에 할당될 수 있다.

```typescript
let name: string;
name = 'junwoo';	// OK
name = null;	// OK
name = undefined; // OK
```



### Strict Null Checking

```
{
	"compilerOptions": {
		"strictNullChecks": true,
		...
	}
}
```

```typescript
let name: string;
name = 'junwoo';	// OK
name = null;	// ERROR
name = undefined; // ERROR
```

<br>

### Union Types 사용하여 Nullable하게 만들기

```typescript
let name: string | null;
name = 'junwoo';	// OK
name = null; // OK
name = undefined; // ERROR
```

`name` 변수는 union type이지만 undefined을 포함하지않기 때문이다.

### example

```typescript
type User = {
	firstName: string;
  lastName: string | undefined;
}

let junwoo: User = { firstName: 'junwoo', lastName: undefined };
let john: User = { firstName: 'john', lastName: 'Doe' };
```

타입 프로퍼티를 옵셔널하게 변경함으로써 같은 효과를 만들 수 있다.

```typescript
type User = {
  firstName: string;
  lastName?: string;
}

//모두 가능하다.
let junwoo: User = { firstName: 'junwoo', lastName: undefined };

let junwoo: User = { firstName: 'junwoo', lastName: 'Doe' };

let junwoo: User = { firstName: 'junwoo' };
```





### Reference

https://mariusschulz.com/blog/non-nullable-types-in-typescript

