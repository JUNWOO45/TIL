---
layout: post
title: vue 기초4 - 데이터바인딩
tags: [vue.js]
comments: true
---

DOM기반 HTML 템플릿에 Vue데이터를 바인딩하는 방법은 크게 3가지가 있습니다.

1.Interpolation(값 대입)

2.Binding Expression(값 연결)

3.Directivces(디렉티브 사용)



<h2>
  Interpolation
</h2>

Vue의 가장 기본적인 데이터 바인딩 체계는 Mustache를 따르는 것입니다.

```
<span>Message: {{ msg }}</span>
<span v-once>This will never change: {{ msg }}</span>
<div v-bind:id="id"></div>
```

<h2>
  Binding Expression
</h2>

Mustache를 이용한 데이터 바인딩을 할때에는 자바스크립트 표현식을 사용할 수 있습니다.

```
<div>{{ num + 1 }}</div>
<div>{{ message.split('').reverse().join('') }}</div>
```

Vue에 내장된 Filter를 Mustache 안에 사용할 수 있습니다.

여러개의 필터 체인도 가능합니다.

```
{{ message | capitalize }}
{{ message | capitalize | upcapitalize }}
```

<h2>
  Directives
</h2>

Vue에서 제공하는 특별한 Attributes이며, -v의 prefix(접두사)를 가집니다.

자바스크립트 표현식, filter 모두 적용됩니다.

```
<p v-if="login">Hello!</p>
<a v-on:click="doSomething"></a>
```