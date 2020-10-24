# Typescript Utils



## Omit

```typescript
interface Student {
  firstName: string;
  lastName: string;
  age: number;
}
```

`Student` 인터페이스에서 age필드는 제외하고, firstName필드와 lastName필드를 사용하는 타입을 만들고 싶을때, 다음과 같이 사용할 수 있다.

```typescript
type Person = Omit<Stuednet, 'age'>
```

<br>

## Exclude

```typescript
interface Student {
  firstName: string;
  lastName: string;
  age: number;
}

interface Subject {
  favorite: string[];
  yearsOfExperience: number;
}

interface Credit {
  type: string;
  level: number;
}

type Person = Student | Subject | Credit;
```

이 중 Person 타입에서 나왔다는 것을 유지하면서, 2가지 타입만 사용하고 싶다면? `Exclude` 를 사용할 수 있다!

```typescript
type SchoolInfo = Exclude<Person, Credit>;
```

<br>

유니온 타입에서도 사용가능하다.

```typescript
type Snacks = 'fruits' | 'vegetables' | 'icecream'

type HealthySnacks = Exclude<Snacks, 'icecream'>
```

