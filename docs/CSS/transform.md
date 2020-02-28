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

<br>

---

## transform-origin

```css
.img {
    transition: transform 0.5s;
    transform-origin: top right;
}

.img:hover {
    transform: rotate(-45deg);
}
```

<br>

---

## 3D transform

두가지를 기억해야하는데, 

부모 엘리먼트에 `perspective` 프로퍼티를 설정해주어야하고, 자신에게는 `translateZ` 프로퍼티를 사용한다.

```css
.container {
    perspective: 1000px;
}

.img {
    transition: transform 1s;
}

.img:hover {
    transform: translateZ(300px);
}
```

`perspective` 프로퍼티는, 우리 눈과 해당 이미지 사이의 거리라고 생각하면 된다.

즉, 마우스를 올리면 1000px에서 300px만큼 다가오게된다. -> '이미지가 커진다' 로 이해하면 됨.

만약, `perspective` 보다 `translateZ` 가 큰 수 이면 어떻게 될까?

우리 눈을 통과해서 이미지가 뒤로 지나가는 꼴.