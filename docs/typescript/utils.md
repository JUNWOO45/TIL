# Typescript Utils

---

## 학습 전, 알고가면 좋은 키워드

### - Union 타입

하나의 프로퍼티에 다양한 변수가 올 수 있는 타입을 의미합니다.

```typescript
// data 변수에는 숫자, 문자를 할당할 수 있습니다.
const data: number | string;

// name 변수에는 문자열 "junwoo", "joonwoo", "junu" 만을 할당할 수 있습니다.
const name: "junwoo" | "joonwoo" | "junu";
```



### - keyof 키워드

타입 값에 존재하는 모든 프로퍼티의 키값들을 유니온 형태로 리턴받습니다.

```typescript
interface Person {
  name: string;
  age: number;
  hobby: string;
  job: string[];
}

// PersonKeys의 타입 = "name" | "age" | "hobby" | "job"
type PersonKeys = keyof Person; 
```





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

<br>

## Partial<T>

> 타입 T의 모튼 프로퍼티를 Optional하게 바꿔줍니다.

```typescript
type Partial<T> = { [P in keyof T]?: T[P]}
```

타입 T의 프로퍼티의 key 값에 해당하는 P를 모두 옵셔널한 형태로 감싸 리턴합니다.



```typescript
interface Person {
  name: string;
  age: number;
  job: string;
}

const user1: Person = {name: 'junwoo', age: 100, job: 'web developer'}; // OK
const user2: Person = {name: 'james', job: 'doctor'};	// Error
const user3: Partial<Person> = {name: 'david', job: 'soccer player'}; // OK
```





---

## Reference

- Omit, Exclude: https://medium.com/@nlemast/typescript-whats-the-difference-between-omit-and-exclude-6d0559ac7c5c
- keyof, Partial: https://medium.com/harrythegreat/typescript-%EC%9C%A0%ED%8B%B8%EB%A6%AC%ED%8B%B0-%ED%81%B4%EB%9E%98%EC%8A%A4-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-7ae8a786fb20