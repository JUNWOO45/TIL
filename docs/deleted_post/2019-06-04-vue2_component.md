---
layout: post
title: vue 기초2 - 컴포넌트 간 통신
tags: [vue.js]
comments: true
---

<h2>
  상위에서 하위로 데이터 전달
</h2>

```
...
<div id="app">
	<child-component v-bind:greeting="message"></child-component>
</div>
...
<script>
	Vue.component('child-component', {
		props: ['greeting'],
		template: '<div>{{greeting}}</div>'
	});
	
	new Vue({
		el: '#app',
		data: {
			message : 'Hello World!'
		}
	});
</script>
```

1. new Vue()로 인스턴스를 하나 생성합니다.
2. Vue.component()로 하위 컴포넌트인 child-component를 등록합니다.
3. child-component의 내용에 props속성으로 greeting을 정의합니다.
4. HTML에 컴포넌트 태그를 추가합니다. child-component태그의 v-bind속성을 보면, v-bind:greeting="message"는 상위 컴포넌트의 message속성 값인 'Hello World'텍스트를 하위 컴포넌트의 greeting으로 전달합니다.
5. child-component의 template속성에 정의된 <div>{{greeting}}</div>는 <div>Hello World</div>가 됩니다.



<h2>
  하위에서 상위 컴포넌트로 이벤트 전달하기
</h2>

```
...
<div id="app">
	<child-component v-on:show-log="printText"></child-component>
</div>

<script>
	Vue.component('child-component', {
		template: '<button v-on:click="showLog">show<button>',
		methods: {
			showLog: function() {
				this.$emit('show-log');
			}
		}
	});
	
	var app = new Vue({
		el: '#app',
		data: {
			message: 'junwoo'
		},
		methods: {
			printText: function() {
				alert('received!')
			}
		}
	});
</script>
```

1. show버튼을 클릭하면, 클릭 이벤트인 v-on:click="showLog"에 따라 showLog()메서드가 실행됩니다.
2. showLog()메서드 안에 this.$emit('show-log')가 실행되면서 show-log이벤트가 발생합니다.
3. show-log이벤트는 <child-component>에서 정의한 v-on:show-log에 전달되고, v-on:show-log의 대상 메서드인 최상위 컴포넌트의 메서드 printText()가 실행됩니다.
4.printText()가 실행됩니다!



<h2>
  이벤트 버스
</h2>

이벤트 버스 형식은 간단히 다음과 같습니다.

```
//이벤트 버스를 위한 추가 인스턴스 1개 생성
var eventBus = new Vue();
```

```
//이벤트를 "보내는" 컴포넌트
methods: {
	메서드명: function() {
		eventBus.$emit('이벤트명', 보낼 데이터);
	}
}
```

```
//이벤트를 "받는" 컴포넌트
methods: {
	created: function() {
		eventBus.$on('이벤트명', function(받는데이터) {
			 ...
		});
	}
}
```



구현은 다음과 같습니다.

```
...
<div id="app">
	<child-component></child-component>
</div>

<script>
	var eventBus = new Vue();
	Vue.component('child-component', {
		template: '<button v-on:click="showLog">show</button>',
		methods: {
			showLog: function() {
				eventBus.$emit('trigger', 500);
			}
		}
	});
	
	var app = new Vue({
		el: '#app',
		created: function() {
			eventBus.$on('trigger', function(value) {
				alert(`value is ${value}`);
			})
		}
	})
</script>
```

1.이벤트 버스로 활용할 새 인스턴스를 1개 생성하고, eventBus라는 변수에 참조합니다.
이제 eventBus라는 변수로 새 인스턴스의 속성과 메서드에 접근할 수 있습니다.

2.하위 컴포넌트에는 template속성과 methods속성을 정의합니다.
template속성에는 show button을 추가하고, methods속성에는 showLog()메서드를 정의하고, 메서드 안에는 eventBus.$emit()을 선언하여 trigger라는 이벤트를 발생하는 로직을 추가합니다.
이 이벤트는 발생할 때 수신하는 쪽에 인자값으로 500이라는 숫자를 함께 전달합니다.

3.상위 컴포넌트의 created 라이프사이클 훅에 eventBus.$on()으로 이벤트를 받는 로직을 선언합니다.
발생한 이벤트 trigger를 수신할 때, 앞에서 전달된 인자값 500이 함께 넘어옵니다.