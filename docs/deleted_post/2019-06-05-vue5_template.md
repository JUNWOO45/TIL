---
layout: post
title: vue 기초5 - 뷰 템플릿
tags: [vue.js]
comments: true
---

뷰의 템플릿은 HTML, CSS등의 마크업 속성과 뷰 인스턴스에서 정의한 데이터 및 로직들을 연결해서 사용자가 브라우저에서 볼 수 있는 형태의 HTML로 변환해주는 속성입니다.

템플릿 속성은 2가지 방법으로 사용할 수 있습니다.

1.ES5에서 뷰 인스턴스의 template속성을 이용하는 방법

```javascript
new Vue({
	template: '<p>hi {{ name }}</p>'
});
```

2.싱글 파일 컴포넌트 체계의 template코드를 활용하는 방법

```
<template>
	<p>hi {{ name }}</p>
</template>
```



참고로,

```javascript
<div id="app">
	<h1>{{message}}</h1>
</div>
<script>
	new Vue({
		el: '#app',
		data: {
			message: 'hi'
		}
	})
</script>
```

```
<div id="app"></div>

<script>
	new Vue({
		el: '#app',
		data: {
			message: 'hi'
		},
		template: '<h1>{{message}}</h1>'
	})
</script>
```

위의 두 코드는 최종적으로 화면에 나타나는 내용은 같습니다.

하지만, 인스턴스의 내용이 적용되는 시점이 다릅니다.

첫번째 코드는 우선 \<h1>{{message}}\<h1>을 화면에 표시합니다.

그 다음에 인스턴스가 생성되면 message의 값을 치환합니다.

두번째 코드는 \<div id="app">에 아무런 내용이 없다가, 인스턴스가 생성되면 \<h1>{{message}}\</h1>이 화면에 달라붙어 표시됩니다.



템플릿에서 사용하는 뷰의 속성과 문법은 다음과 같습니다.

- 데이터 바인딩
- 자바스크립트 표현식
- 디렉티브
- 이벤트 처리
- 고급 템플릿 기법

<h3>
  데이터 바인딩
</h3>

데이터 바인딩은 HTML화면요소에 뷰 인스턴스의 데이터를 연결하는 것을 의미합니다.

Mustache문법과 v-bind속성이 있습니다.



Mustache는 생략하고,

```
<div id="app" v-once>{{message}}</div>
```

아, v-once는 기억할것!



v-bind는 아이디, 클래스, 스타일등의 HTML속성(attributes)값에 뷰 데이터 값을 연결할 때 사용하는 데이터 연결 방식입니다.

```
<div id="app">
	<p v-bind:id="idA">id binding</p>
	<p v-bind:class="classB">class binding</p>
	<p v-bind:style="styleC">style binding</p>
</div>

<script>
	new Vue({
		el: '#app',
		data: {
			idA: 'my_id',
			classB: 'my-class',
			styleC: 'color: red'
		}
	});
</script>
```

v-bind:문법을 :로 간소화 할 수 있습니다.

```
<div v-bind:id>
는
<div :id>
와 같습니다.
```



<h3>
  자바스크립트 표현식
</h3>

Mustache안에 자바스크립트 표현식을 넣으면 됩니다.

```
<div id="app">
  <p>{{message + '!!'}}</p>
  <p>{{message.split('').reverse().join('')}}</p>
</div>
<script>
  new Vue({
    el: '#app',
    data: {
    	message: 'junwoo'
    }
  })
</script>
```

주의할 점이 있습니다.

1.자바스크립트의 선언문과 분기구문은 사용할 수 없습니다.

2.복잡한 연산은 인스턴스 안에서 처리하고, 화면에는 간단한 연산결과만 표시해야합니다.

```
<div id="app">
  {% raw %}{{ var a = 10; }}{% endraw %} 선언문은 사용불가능.
  {% raw %}{{ if(isTrue) {return 'This is true!!'} }}{% endraw %} 분기구문 불가능
  {% raw %}{{ isTrue ? 'This is true!!!' : 'This is false..' }}{% endraw %}삼항연산자는 가능
  
 {% raw %}{{ message.split('').reverse().join('') }}{% endraw %}복잡한 연산은 인스턴스에서!
  {% raw %}{{ reversedMessage }}{% endraw %} 이런식으로!
</div>

<script>
	new Vue({
		el: '#app',
		data: {
			message: 'junwoo!!!'
		},
		computed: {
			reversedMessage: function() {
				return this.message.split('').reverse().join('');
			}
		}
	})
</script>
```



<h3>
  디렉티브
</h3>

뷰 디렉티브란 HTML태그 안에 v-접두사를 가지는 모든 속성들을 의미합니다.

v-bind속성도 디렉티브에 해당됩니다.

```
<a v-if="flag">누누!</a>
```

주요 디렉티브는 다음과 같습니다.

- v-if
- v-for(지정한 뷰 데이터의 갯수만큼 해당 HTML태그를 반복 출력합니다.)
- v-show(v-if와 마찬가지로 데이터의 진위여부에 따라 해당 HTML태그를 화면에 표시하거나 표시하지 않습니다.다만, v-if는 해당 태그를 완전히 삭제하지만 v-show는 css효과만 display:none으로 바꿔서 실제 태그는 남아있고 화면상으로만 보이지않습니다.)
- v-bind(HTML태그의 기본 속성과 뷰 데이터 속성을 연결합니다.)
- v-on(이벤트를 감지하여 처리합니다.)
- v-model(form에서 주로 사용되는 속성입니다. 폼에 입력한 값을 뷰 인스턴스의 데이터와 즉시 동기화합니다. 화면에 입력된 값을 저장하여 서버에 보내거나, watch와 같은 고급 속성을 이용하여 추가 로직을 수행할 수 있습니다. input, select, textarea태그에만 사용할 수 있습니다.)

<h3>
  이벤트처리
</h3>

```
<button v-on:click="clickBtn">btn</button>

methods: {
	clickBtn: function() {
		window.alert('clicked!');
	}
}
```

다음처럼 인자 값을 넘기는 방법또한 있습니다.

```
<button v-on:click="clickBtn('hi')">btn</button>

methods: {
	clickBtn: function(greeting) {
		window.alert('clicked!' + greeting + '!!!!');
	}
}
```

<h3>
  고급 템플릿 기법
</h3>

: 실제 어플리케이션을 개발할 때 유용한 속성으로, 앞에서 공부한 데이터 바인딩, 디렉티브와 같은 기본적인 문법과 함께 사용된다고 합니다.

<h4>
  computed속성
</h4>

앞에서 공부했듯이, 데이터를 가공하는 등의 복잡한 연산은 뷰 인스턴스 안에서 하고, 최종적으로 HTML에는 데이터를 표현하기만 한다고 했습니다.

computed속성은 이러한 데이터 연산들을 정의하는 영역입니다.

```
<div id="app">
	<p>{{ reversedMessage }}</p>
</div>

<script>
	new Vue({
		el: '#app',
		data: {
			message: 'junwoo'
		},
		computed: {
			reversedMessage: function() {
				return this.message.split('').reverse().join('');
			}
		}
	})
</script>
```

computed속성의 첫번째 장점은 data속성값의 변화에따라 자동으로 다시 연산이 된다는 점입니다.

두번째 장점은 캐싱입니다.

캐싱은 동일한 연산을 반복해서 하지 않기 위해 연산의 결과 값을 미리 저장하고 있다가 필요할 때 불러오는 동작입니다.

지금 예제에서는 reversedMessage값을 한번만 표현했지만, 만약 화면의 다른곳에서도 같은 값을 표시해야한다면 computed속성의 reversedMessage()가 미리 연산한 결과를 가지고 있다가화면에 결과를 표시하게됩니다.

<h4>
  computed속성과 methods속성의 차이점
</h4>

우선, 가장 큰 차이점은 methods속성은 호출이 될 때에만 해당 로직이 수행되고, computed속성은 대상 데이터값이 변경되면 자동으로 수행된다는 점입니다.

다시말해 수동적으로 데이터를 갱신하느냐, 능동적으로 데이터를 갱신하느냐의 차이점입니다.

이러한 점의 연장선상에서, methods속성은 수행할 때마다 연산을 하기 때문에 별도의 캐싱을 하지 않습니다.

하지만 computed속성은 데이터가 변경되지않는 한 이전의 계산값을 가지고 있다가 필요할 때 바로 반환해줍니다.

따라서, 복잡한 연산을 반복해서 수행해야한다면 methods속성보다는 computed속성을 사용하는 것이 성능면에서 훨씬 효율적입니다.



<h4>
  watch속성
</h4>

watch속성은 데이터 변화를 감지하여 자동으로 특정 로직을 수행합니다.

computed속성과 유사하지만, computed속성은 내장API를 활용한 간단한 연산 정도가 적합한 반면, watch속성은 데이터 호출과같이 시간이 상대적으로 더 많이 소모되는 비동기처리에 적합합니다.

```
<div id="app">
	<input v-model="message">
</div>

new Vue({
	el: '#app',
	data: {
		message: 'junwoo vue!'
	},
	watch: {
		message: function(data) {
			console.log('message의 값이 바뀝니다 : ', data)
		}
	}
})
```