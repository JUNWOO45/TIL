# Observable



promise는 pull한 느낌이고 observable은 push스러운 느낌이다.

```typescript
new Observable(subscriber => {
  
})
```

이 subscriber한테 값을 전달해주는거다. (이래서 push스러운 느낌이라고..)

```typescript
new Observable(subscriber => {
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
new Observable(subscriber => {
  console.log('worked');
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
}).subscribe()

// worked
```



 이 `subscribe` 에게는 `observer` 를 전달하게 됩니다.

```typescript
new Observable(subscriber => {
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
new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
}).subscribe({
  next() {},
  error() {},
  complete() {}
})
```

`옵저버블` 의 콜백함수에서 실행되는 `next` 메소드는, `subscribe` 의 `next` 에서 값을 받아온다.

```typescript
new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
}).subscribe({
  next(value) {
    console.log(value);
  },
  error() {},
  complete() {}
})

//1 2 3
```

---

`subscriber` 를 `옵저버` 로 이해하면된다.

```typescript
new Observable(observer => {
  observer.next(1);
  observer.next(2);
  observer.next(3);
}).subscribe()
```

`옵저버블` 의 콜백함수에서 비동기적인 코드를 작성할 수도 있다.

```typescript
new Observable(observer => {
  setTimeout(() => {
    observer.next('자라나라머리머리');
  }, 1000)
}).subscribe({
  next(value) {
    console.log(value);
  }
})

//자라나라머리머리
```



하나의 `옵저버블` 에 여러개의 `옵저버` 실행시킬 수 있다.

원천적인 데이터는 하난데, 이 데이터를 처리하는 로직이 두가지인 그런 느낌.

```typescript
const observable = new Observable(observer => {
  setTimeout(() => {
    observer.next('자라나라머리머리');
  }, 1000)
});

//첫번째 옵저버
observable.subscribe({
  next(value) {
    console.log('1', value);
  }
});

//두번째 옵저버
observable.subscribe({
  next(value) {
    console.log('2', value);
  }
});
```

<br>

`옵저버블` 을 종료하려면 `next` 메소드처럼 `complete` 메소드를 사용하면 된다.

```typescript
new Observable(observer => {
  observer.next(123123);
  observer.complete();
}).subscribe({
  next(value) {
    console.log(value);
  },
  error(){},
  complete() {
    console.log('is completed');
  }
});
```



`subscribe ` 에 지금처럼 `옵저버 객체` 를 전달할 수 도 있지만, 순서대로 next, error, complete 콜백을 넣어도 된다.

```typescript
new Observable(observer => {
  observer.next(123123);
  observer.complete();
}).subscribe(value => {
  console.log(value);
}, error => {
  console.error(error);
}, () => {
  console.log('is completed');
});
```

