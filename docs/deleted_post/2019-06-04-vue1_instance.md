---
layout: post
title: vue 기초1 - 뷰 인스턴스
tags: [vue.js]
comments: true
---

모든 Vue앱은 Vue함수로 새로운 뷰 인스턴스를 만드는 것부터 시작합니다.

```
var vm = new Vue({
	//option...
})
```

뷰 인스턴스를 인스턴스화할때에는, 데이터, 템플릿, 마운트할 엘리먼트, 메소드, 라이프사이클 콜백 등의 옵션을 포함할 수 있는 options객체를 전달해야합니다.

모든 뷰 컴포넌트는 본질적으로 확장된 뷰 인스턴스입니다.

<h4>
  속성과 메소드
</h4>

각 뷰 인스턴스는 data객체에 있는 모든 속성을 프록시처리합니다.

```
var data = { a : 1 };

var vm = new Vue({
	data: data
});

vm.a === data.a;	//true

vm.a = 5;
data.a;	// 5

data.a = 10;
vm.a;	//10

```

데이터가 변경되면, 화면은 다시 렌더링됩니다.

유의할 점은, data에 있는 속성들은 인스턴스가 생성될 때 존재한 것들만 반응형이라는 점입니다.

즉, 다음처럼 새 속성을 추가한다면..

```
vm.b = 'hi?';
```

b가 이후에 변경되더라도 화면은 갱신되지않습니다.

따라서, 어떠한 속성이 나중에 필요하다는 것을 알고 있다면... 다음처럼 data를 처음부터 지정해주는 것이 좋습니다.

```
data : {
	name: '',
	age: 0,
	todos: [],
	error: null
}
```
