# Animation



```css
div {
  width: 150px;
  height: 150px;
  background-color: blue;
  animation-name: moving;
}

@keyframes moving {
  from { transform: translateX(0); }

  to { transform: translateX(1000px); }
}
```

함수라고 생각하면 된다.

```css
@keyframes moving {
  0% { transform: translateX(0); }

  100% { transform: translateX(1000px); }
}
```

이렇게 적어도 된다

```css
@keyframes moving {
  0% { transform: translateX(0); }

  80% { transform: translateX(1000px); }

  100% { transform: translate(1000px, -150px); }
}
```

각도를 꺾는 것도 가능하다.

<br>

### animation-duration

```css
div {
  ...
  animation-duration: 4s;
}
```

이렇게 duration을 정할 수 있다.

<br>

### animation-fill-mode 

Animation이 끝나면, 처음 위치로 엘리먼트가 이동하는 것을 볼 수 있다.

(상당히 신경쓰인다..)

애니메이션의 100% 위치에 도달한 곳에 엘리먼트를 계속 위치시킬 수 있다.

```css
div {
  ...
  animation-fill-mode: forwards;
}
```

default는 `none`인데, `backwards` 와 `both` 또한 존재한다.

얘네는 `animation-delay` 와 `animation-duration` 을 섞어서 무언가를 만들어낼 때 사용하는 듯하다.

<br>

### animation-delay

`transition-delay` 와 같다.

설정해준 시간이 지난 후 애니메이션이 발동한다.

```css
div {
  ...
  animation-delay: 2s;
}
```

<br>

### animation-iteration-count

애니메이션 반복 횟수

```css
div {
  animation-iteration-count: 3;
}
```

무한반복도 가능하다.

```css
div {
  animation-iteration-count: infinite;
}
```

<br>

### animation-timing-function

어떤 패턴으로 애니메이션이 발동할지. transition과 같다.

```css
div {
  ...
  animation-timing-function: ease-in;
}
```

<br>

### animation-direction

애니메이션 방향을 결정한다.

`reverse` 로 설정하면 역순으로 애니메이션이 실행된다.

default는 `normal` 이다.

```css
div {
  ...
  animation-direction: reverse;
}
```

재미있는 `alternate` 도 있다.

```css
div {
  ...
  animation-direction: alternate;
}
```

0% -> 100% -> 0% -> 100% -> .... 계속 반복한다!

`alternate-reverse` 도 있다.

<br>

### animation-play-state

정신사나울때 끌 수 있다..

```css
div {
  ...
  animation-play-state: paused;
}
```

<br>

이러한 모든 속성들을 `animation` 메소드에서 바로 가능

```css
div {
  ...
  animation: moving 3s both 3 ease-in alternate 1s;
}
```

대체로 순서는 상관이 없지만, 상관있는게 하나 있다.

`delay time` 은 무조건 `duration time` 다음에 위치해야한다.

처음 3s는 `duration time` 이고, 가장 마지막 1s는 `delay time` 이다.