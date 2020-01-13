# Observable



promise는 pull한 느낌이고 observable은 push스러운 느낌이다.

```typescript
const observable = new Observable(subscriber => {
  
})
```

이 subscriber한테 값을 전달해주는거다. (이래서 push스러운 느낌이라고..)

```typescript
const observable = new Observable(subscriber => {
  console.log('worked');
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
})
```



위 코드는 동작하지않는다.

observable에게는 promise를 사용할때 값을 받을수있는 `then` 과 같은, `subscribe` 가 있다.

이 `subscribe` 가 있어야, Observable에 넘겨준 콜백함수가 동작한다.

```typescript
const observable = new Observable(subscriber => {
  console.log('worked');
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
}).subscribe()

// worked
```



 이 `subscribe` 에게는 `observer` 를 전달하게 됩니다.

```typescript
const observable = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
}).subscribe(여기에 옵저버를 전달합니다.)
```

 `observable` 에서는 일련의 데이터를 계속 생성해내고, `observer` 에서는 이 데이터를 읽어올 수 있다.

---

> 정리를 한 번 하고 가면, " `옵저버블` 은 `subscribe` 를 해야만 실행된다." 정도로 요약할 수 있을 듯하다.

<br>

`옵저버` 에는 next, error, complete의 3가지 메소드가 존재한다.



```typescript
const observable = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
}).subscribe({
  next() {},
  error() {},
  complete() {}
})
```

