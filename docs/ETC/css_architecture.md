# CSS Architecture



## - BEM

- Block Element Modifier
- ex) header__form--email



### Block(전체를 감싸고 있는 블럭요소)

- 독립적으로 의미가 있는 컴포넌트를 의미합니다.

```html
<div class="block">...</div>
```



- header, footer, nav, main등의 컨텐츠 영역을 block으로 간주할 수 있습니다.

  ![bem1](../pic/css_architecture1.jpeg)

  

- 더 구체적으로, header block은 logo block, search form block, authorization block을 포함할 수 있습니다.

  ![bem2](../pic/css_architecture3.png)

- block은 클래스의 어근을 형성하고, 항상 맨 앞에 위치합니다.



### Element

- 독립적으로는 의미가 없으며 Block에 붙어서 사용되는 컴포넌트를 의미합니다.

```html
<div class="block">
  <span class="block__element">...</span>
</div>
```

- element는 block이 포함하고 있는 한 조각입니다.
- 예를 들어 위에서 보았던 block이미지에서, menu item은 menu block 바깥에서는 사용될 수 없습니다.
  따라서 각각의 메뉴아이템은 element입니다.

![bem3](../pic/css_architecture4.png)

- 두개의 underscore로 연결하여 블럭 다음에 위치시킵니다.

```css
.block__element {
	display: none;
}
```

```css
.header__logo {
  property: value;
}

.header__tagline {
  property: value;
}

.header__navigation {
  property: value;
}
```



### Modifiers

- modifier는 block 또는 element의 속성입니다.

  이 속성은 block이나 element의 외관이나 상태를 변화시킵니다.

  기본적으로, class명은 반복하여 재사용할 수 있게 하기위해 존재합니다.

  특정 요소의 스타일을 수정해야할 필요가 있을때 modifier를 활용하게 됩니다.

  이때, element나 block다음에 두개의 하이픈'--'을 추가하여 modifier를 표시합니다.

```css
.block__element--modifier {
  display: none;
}
```

- 다음처럼 focused된 tab3를 modifiers라고 볼 수 있습니다.

![bem4](../pic/css_architecture5.png)



### 사용 예

- 다음과 같은 버튼을 만든다고 하면,

![bem5](../pic/css_architecture2.jpeg)

```html
<button class="button">
  Normal button
</button>
<button class="button button--state-success">
  Success button
</button>
<button class="button button--state-danger">
  Danger button
</button>
```

```css
.button {
  display: inline-block;
	border-radius: 3px;
	padding: 7px 12px;
	border: 1px solid #D5D5D5;
	background-image: linear-gradient(#EEE, #DDD);
	font: 700 13px/18px Helvetica, arial;
}
.button--state-success {
  color: #FFF;
	background: #569E3D linear-gradient(#79D858, #569E3D) repeat-x;
}
.button--state-danger {
  color: #900;
}
```





공부, 그림 출처

- http://getbem.com/faq/
- https://blog.theodo.com/2015/10/how-i-stopped-worrying-and-learned-to-love-the-css-with-bem/
- https://en.bem.info/methodology/key-concepts/
- https://webclub.tistory.com/263
- https://blog.naver.com/PostView.nhn?blogId=dilrong&logNo=221496133579

