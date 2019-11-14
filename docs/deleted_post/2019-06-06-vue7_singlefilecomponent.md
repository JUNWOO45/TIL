---
layout: post
title: vue 기초7 - 싱글파일 컴포넌트
tags: [vue.js]
comments: true
---

<h3>
  with JSX(ES6)
</h3>

<h3>싱글 파일 컴포넌트 체계란, 한마디로 확장자 .vue파일로 프로젝트 구조를 구성하는 방식을 말합니다.</h3>


앱의 복잡도가 증가할때, .vue라는 파일 단위 안에 html, js, css를 관리할 수 있는 방법.

복잡도가 커짐에 따라 야기될 수 있는 문제들

- 모든 컴포넌트에 고유의 이름을 붙여야함
- js파일에서 template안의 htmldml 문법강조가 되지않음.
- js파일에서 css스타일링 작업이 거의 불가
- ES5를 이용하여 계속 앱을 작성할 경우 Babel빌드가 지원되지않음.

.vue파일을 브라우저가 렌더할 수 있는 파일들로 변환하려면 webpack의 vue-loader 또는 browserify를 이용.

```
<template>
	...
</template>

<script>
	...
</script>

<style>
	...
</style>
```