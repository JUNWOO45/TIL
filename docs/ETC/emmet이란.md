

<h1>
  emmet이란!
</h1>

엄청엄청 유명한 텍스트에디터 플러그인입니다!

html이나 css등을 작성할때 시간을 단축시켜주는 확장기능입니다!

<h2>
  하위
</h2>

```
div>ul>li
```

를 입력하면,

```html
<div>
  <ul>
    <li></li>
  </ul>
</div>
```

이렇게 코드가 생성됩니다!

'>'는 하위에 태그를 생성하라는 의미입니다.



<h2>
  병렬
</h2>

```
div+p+div
```

를 입력하면,

```html
<div></div>
<p></p>
<div></div>
```

코드가 생성됩니다.



## 반복

```
ul>li*5
```

를 입력하면,

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

이렇게 코드가 생성됩니다!



## class나 id넣기

```
ul>li.item*3
```

을 입력하면

```html
<ul>
  <li class="item"></li>
  <li class="item"></li>
  <li class="item"></li>
</ul>
```

이렇게 입력됩니다!

id는 . 대신에 #을 넣어주면 됩니다!