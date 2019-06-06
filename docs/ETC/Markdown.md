<h1>
  Markdown
</h1>



매일매일 TIL을 진행하면서 [Typora](<https://typora.io/>)를 사용했습니다.

깔끔한 디자인이 너무나 맘에 들었어요.

하지만 항상 사용하던 마크다운 문법만 사용하고… 필요할때 검색을 하다가, 한번 정리를 해봐야겠다는 생각이 들어서 공부겸 이렇게 기록으로 남깁니다..!

<hr>

##heading

우선, \<h1>,\<h2>,\<h3>,\<h4>,\<h5>,\<h6>태그는, \#을 이용합니다.

\#의 갯수와 heading태그의 number가 일치하죠!

#heading 1

```
#heading 1
```

## heading 2

```
##heading 2
```

### heading 3

####heading 4

#####heading 5

######heading 6

<hr>

## Text



**Bold text**

```
**Bold text**
```

*Italic text*

```
*Italic text*
```

~~Strike through~~

```
~~Strike through~~
```

<mark>Marked text</mark>

```
<mark>Marked text</mark>
```

<pre>Preformatted text</pre>

```
<pre>Preformatted text</pre>
```

<small>Small text</small>

```
<small>Small text</small>
```

This is <sub>subscript</sub>

```
This is <sub>subscript</sub>
```

This is <sup>superscript</sup>

```
This is <sup>superscript</sup>
```

<hr>

## Links

[인라인 링크](https://google.com)

```
[인라인 링크](https://google.com)
```



<hr>

## Lists

이건 간단합니다. "숫자+dot+space"과 "- + space"...

그러니 안써본걸 적어봐야져..!

- [x] Task1

- [ ] Task2
  - [x] Subtask A
  - [ ] Subtask B

```
- [x] Task1
- [ ] Task2
	- [x] Subtask A
	- [ ] Subtask B
```

중요한 하이픈( - )다음에 한칸 띄어주어야 한다는 것..!

<hr>

## Blockquotes

인용문입니다.. 이런것도 되는군요..!



> 웹서핑을 하면서 자주 보던 형식입니다.
>
> 중요한 것은 '내가 무엇을 모르는지' 아는 상태가 되어야 한다고 들었는데,
>
> 이러한 기능이 마크다운에서 가능한지조차 모르고 있었죠.
>
> 그래서 찾아보려고조차 안했는데… 너무 멋진 기능입니다!!

```
> 웹서핑을 하면서 자주 보던 형식입니다.

> 중요한 것은 '내가 무엇을 모르는지' 아는 상태가 되어야 한다고 들었는데,

> 이러한 기능이 마크다운에서 가능한지조차 모르고 있었죠.

> 그래서 찾아보려고조차 안했는데… 너무 멋진 기능입니다!!
```

<hr>

## Code

`인라인 코드`는 이렇게 씁니다.

```
`인라인 코드`는 이렇게 씁니다.
```



```javascript
const add = (num1, num2) => num1 + num2;
console.log(add(3, 4));	//7
```

```
​```javascript
const add = (num1, num2) => num1 + num2;
console.log(add(3, 4)); //7
​```
```

와우, 항상 \`\`\`만 사용했었는데 뒤에 javascript를 설정할 수 도 있네요…!

```html
<body>
  <p>
    오토태그기능까지 내장되어 있다니..!
  </p>
</body>
```

```
​```html
<body>
	<p>오토태그기능까지 내장되어 있다니..!</p>
</body>
​```
```

놀라운 기능이네요… 까먹지말고 자주 써먹어야겠습니다!!!

<hr>

## Keyboard

HTML unicode utf-8을 사용해서 여러 버튼들을 표시할 수 있습니다.

<kbd>&uarr;</kbd>Arrow Up

```
<kbd>&uarr;</kbd> Arrow Up
```

<kbd>&#8984;</kbd> Command

```
<kbd>&#8984;</kbd> Command
```

<kbd>&#8677;</kbd> Tab

```
<kbd>&#8677;</kbd> Tab
```



신기할 따름입니다..

---

## Horizontal Rule

저는 항상 \<hr>태그를 사용했었는데요. 앞으로는 사용안할겁니다.ㅎㅎ

```
---
```

---

## Emoji

저도 요즘 많이 쓰려고하고, 관심있어하는 **이모지**입니다..!

:smirk:

```
:smirk:
```

:scream:

```
:scream:
```

여기서 이모지목록을 확인할 수 있습니다 : [이모지 치트시트](https://www.webfx.com/tools/emoji-cheat-sheet/)

















