---
layout: post
title: vue 기초6 - 클래스 바인딩
tags: [vue.js]
comments: true
---

<h3>
  크게 2가지 방법으로 나뉘지만, 공통점은 v-bind:class를 사용합니다.
</h3>



1.

```
<div class="static" v-bind:class="{'red-color': isA, 'blue-color': isB}"></div>
```

```
data: {
	isA: true,
	isB: false
}
```

2.

```
<div v-bind:class="[greenColor, yellowColor]"></div>
```

```
data: {
	greenColor: 'green-color',
	yellowColor: 'yellow-color'
}
```