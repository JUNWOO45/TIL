# LESS

LESS는 CSS에 Script능력(변수, 함수, 연산, 중첩, 스코프 등)을 덧붙여 확장한 언어입니다.

LESS는 클라이언트 또는 서버환경(node.js)에서 모두 실행가능합니다.

CSS Preprocessor(CSS 전처리기)로서 쉽고 빠르고 체계적으로 프로그래밍할 수 있도록 해줍니다!



<h2>
  Variables
</h2>

```css
@width: 100px;
@height: @width - 50px;

.test1 {
  width: @width;
  height: @height;
}
```

Outputs:

```css
.test1 {
  width: 100px;
  height: 50px;
}
```



## Mixins

```css
.bordered {
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}

.test2 {
  color: red;
  .bordered();
}

.test3 {
  color: blue;
  .bordered();
}
```

Output:

```css
.bordered {
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}

.test2 {
  color: red;
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}

.test3 {
  color: blue;
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}
```

> 믹스인을 **호출**할 때, 괄호는 옵션입니다!
>
> .bordered(); === .bordered;

<h3>
  믹스인 출력 막기
</h3>

믹스인을 만들고는 싶지만, 그 믹스인을 지금 출력할 필요가 없을때에는 뒤에 괄호를 넣으면 됩니다.

```css
.my-mixin {
  //괄호가 붙지않은 믹스인은 컴파일됩니다!
  color: black;
}

.my-other-mixin() {
  //괄호가 붙은 믹스인은 css파일에 컴파일되지 않습니다!
  background-color: gray;
}

.demo {
  .my-mixin();
  .my-other-mixin();
}
```

Output:

```css
.my-mixin {
  color: black;
}

.demo {
  color: black;
   background-color: gray;
}
```

### 네임스페이스

```css
#outer {
  .inner {
    color: red;
  }
}

.other {
  #outer > .inner;
}
```

Output:

```css
#outer .inner {
  color: red;
}

.other {
  color: red;
}
```

> 모두 같은 결과입니다.
>
> \#outer > .inner;
>
> \#outer .inner;
>
> \#outer.inner;

<h2>
  Nesting
</h2>

```css
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```

Output:

```css
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```

가상선택자를 사용할 수 있습니다.

**&기호는 바로 위의 부모 선택자를 가리킵니다!**

```css
.parent {
  display: block;
  color: red;
  &:hover {
    font-size: 50px;
    color: orange;
  }
}
```

Output:

```css
.parent {
  display: block;
  color: red;
}
.parent:hover {
  font-size: 50px;
  color: orange;
}
```



## Operations

```css
//숫자들은 같은 단위로 변환됩니다.
@conversion01: 5cm+10mm;	//6cm
@conversion02: 2 - 3cm - 5mm	//-1.5cm
  
//변환 불가능!
@imposibble01: 2 + 5px - 3cm;	// 4px

//example
@base: 5%;
@filler: @base * 2;	//10%
@other: @base + @filler //15%
```

```css
@var: 1px + 5 //6px
@width: (@var + 5) * 2;

.operation {
  width: @width;
  border: (@width / 11) solid black;
}
```

Output:

```css
.operation {
  width: 22px;
  border: 2px solid black;
}
```

