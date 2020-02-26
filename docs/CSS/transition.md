# Transition



### transition-timing-function

5개가 있다.

- ease
- linear
- ease-in
- ease-out
- ease-in-out



### transition-delay

지정한 ms 또는 s 이후에 트랜지션이 실행된다.



### transition-duration

ㅇㅇ duration.

---

```css
button {
  .
  .
  .
  transition: {
    background-color 3s ease 1s,
    color 2s ease-in 4s,
    border-radius 2s linear 6s
  }
}

button:hover {
  background-color: orange;
  color: white;
  border-radius: 50%;
}
```

이런 식으로 각각의 property들을 독립적으로 트랜지션시킬 수 있음.

```css
button {
  .
  .
  .
  transition: {
    all 3s ease-in 1s
  }
}

button:hover {
  background-color: orange;
  color: white;
  border-radius: 50%;
}
```

간단하게 `all` 로 모든 프로퍼티들을 변경시킬 수 있지만, 트랜지션의 시작과 끝이 동일함. ㅇㅇ 변화가 동시에 일어나고 동시에 끝나게됨.