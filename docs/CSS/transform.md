# Transform

- scale
- translate
- rotate
- skew



---

`transition` 에 의해 발동된다.

```css
.img {
    transition: transform 2s ease-out;
}

.img:hover {
    transform: translate(500px, -400px);
}
```

`transition` 에서는 변화를 주고싶은 프로퍼티를 적는다.

ex)

```css
transition: color 2s linear 1s;

.btn:hover {
  color: red;
}
```

프로퍼티로 `transform` 을 선택했다고 생각하면 되겠다.

