# Iterable이란?

- string이나 array같이 무언가를 담고있는 것의 행위에 대한 약속.
  - "순회를 할 수 있다..!"
- 즉 문자열과 배열은 iterable이다.
- iterable은 for...of 와 spread 연산자를 사용할 수 있다.

```typescript
for(const i in [1, "a", 3]) {
  console.log(i);
}
//0 1 2

for(const i of [1, "a", 3]) {
  console.log(i);
}
//1 "a" 3
```

- for in 같은 경우 보통 object의 key값을 가져오는데 사용하는데,
  for of는 item을 들고오기위해 사용한다.
  왜 for...of를 사용할 수 있는걸까?
  배열이라서?
  아니. 이터러블이라서 사용할 수 있는거 ㅇㅇ



```typescript
const prices = [100, 200, 300];
const lowestPrice = Math.min(prices);

const sayGoodBye = ['b', 'y', 'e'];
console.log('sayGoodBye : ', sayGoodBye);
console.log(['say', ...sayGoodBye, '!']);
```



