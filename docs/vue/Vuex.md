<h1>
  Vuex
</h1>



<h3>
  Vuex 사용하기
</h3>

우선 Vuex를 설치합니다.

```
$ npm install vuex --save
```

Vuex를 등록한 js파일을 하나 생성합니다.

컨벤션에따라 store.js로 해줍시다!

```
// store.js

import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
	state: {
		counter: 0
	}
});
```

Vue와 App이 등록된 main.js에서 store.js를 불러와 등록해줍니다.

```
//main.js

import Vue from 'vue';
import App from './App.vue'
import { store } form './store'

new Vue({
	el: '#app',
	store,
	render: h => h(App)
})
```

App.vue에서 Vuex를 사용해봅니다. state에 등록된 counter에 접근하려면 **this.$store.state.counter** 를 사용합니다.

```
//App.vue

<template>
  <div id="app">
    counter: {{ this.$store.state.counter }}
    <button @click="add">+</button>
    <button @click="sub">-</button>
  </div>
</template>

<script>
	export default {
		methods: {
			add() {
				this.$store.state.counter++;
			},
			sub() {
				this.$store.state.counter--;
			}
		},
		components: {
			'child': Child
		}
	}
</script>
```



<h3>
  Getters란?
</h3>

중앙 데이터 관리식 구조에서 발생하는 문제점 중 하나는 각 컴포넌트에서 Vuex의 데이터를 접근할때 중복된 코드를 반복호출하게된다는 점입니다.

```
// App.vue
computed: {
	add() {
		return this.$store.state.counter++;
	}
}
```

```
// Child.vue
computed: {
	add() {
		return this.$store.state.counter++;
	}
}
```

복수개의 컴포넌트에서 똑같은 로직을 반복하고 있습니다.

이때, Vuex의 데이터(state)변경을 각 컴포넌트에서 수행하는 것이 아니라, Vuex에서 수행하도록하고 각 컴포넌트에서 수행로직을 호출하면, 코드 가독성도 올라가고 성능에서도 이점이 생깁니다!

```
// store.js(Vuex)
getters: {
	add:function(state) {
		return state.counter++;
	}
}
```

```
//App.uve
computed: {
	add() {
		return this.$store.getters.add;
	}
}
```

```
//Child.vue
computed: {
	add() {
		return this.$store.getters.add;
	}
}
```

만약 getters에 담겨있는 함수가 엄~~청 복잡하다면, 왜 Getters를 쓰는게 편한지 더욱 체감할 수 있을 듯 싶습니다.

```
//store.js
export const store = new Vuex.Store({
	state: {
    counter: 0
  },
	getters: {
		getCounter: function(state) {
			return state.counter;
		}
	}
})

```

```
//App.vue
<div id="app">
	Parent counter: {{ parentCounter }}
</div>

<script>
	computed: {
		parentCounter() {
			return this.$store.getters.getCounter;
		}
	}
</script>
```

```
//Child.vue
<div>
	Child counter: {{ childCounter }}
</div>

<script>
	computed: {
		childCounter() {
			return this.$store.getters.getCounter;
		}
	}
</script>
```

1.우선, 기존에 Parent counter: {{ this.$store.state.counter }}라고 쓰여있던건 너무 깁니다!

template의 표현식은 최대한 간소화해야한다고 공부했습니다. 고쳐줍니다.

2.Vuex에 Getters를 등록해줍니다.

그리고 기존의 parentCounter와 childCounter에 사용되던 return this.\$store.state.counter를 return this.\$store.getters.getCounter로 고쳐줍니다.

<h3>
  mapGetters
</h3>

mapGetters는 Vuex에 내장된 helper함수입니다.

getters를 써서 가독성이 올라간 코드를 더 직관적으로 작성할 수 있게 도와줍니다.

```
//App.vue
<div id="app">
  Parent counter : {{ parentCounter }}
</div>
```

이걸..

```
//App.vue
import { mapGetters } from 'vuex';

// ...
computed: mapGetters({
	parentCounter: 'getCounter'
})
```

getCounter는 Vuex의 getters에 선언된 속성이름입니다.



<h3>
  Mutations
</h3>

Mutations는 Vue의 데이터, 즉 state값을 변경하는 로직을 의미합니다.

Mutations는 Getters와는 다르게,

1.인자를 받아 Vuex에 넘겨줄 수 있습니다.

2.computed가 아닌 methods에 등록합니다.

지금까지는 

```
return this.$store.state.counter++;
return this.$store.state.counter
```

처럼 직접 state에 접근하여 데이터를 다루었지만, 이것은 **안티패턴**입니다..!

(그 이유는, 여러개의 컴포넌트에서 같은 state값을 동시에 제어하게된다면, state값이 어느 컴포넌트에서 호출해서 변경된것인지 추적하기 어렵기때문입니다.)

<h3>
  Mutations등록</h3>

```
//store.js

export const store = new Vuex.Store({
	//...
	mutations: {
		addCounter: function(state, payload) {
			return state.counter++;
		}
	}
})
```

<h3>
  Mutations사용
</h3>

```
//App.vue
methods: {
	addCounter() {
		this.$store.commit('addCounter');
	}
}
```

Mutations는 commit을 이용해서 접근해야합니다.



<h3>
  Mutations에 인자 값 넘기기
</h3>

각 컴포넌트에 state를 조작하는데 필요한 특정값들을 넘기고싶을때엔 commit()의 두번째 인자를 넣어줍니다.

```
this.$store.commit('addCounter', 10);
this.$store.commit('addCounter', {
	age: 100,
});
```

두번째 예시를 Vuex에서 받는다고 가정하면..

```
mutations: {
	//this.$store.commit('getAge', {
	//	age: 100
	//})
	getAge: function(state, payload) {
		state.age = payload.age;
	}
}
```



<h3>
  Actions란?
</h3>

Mutations에는 순차적인 로직들만 선언하고, Actions에는 비순차적 또는 비동기적 처리로 로직들을 선언합니다.

왜이렇게 Mutations와 Actions로 나눠서 등록할까요?

Mutations는 State관리에 주안점을 두고 있습니다.

**"상태관리"**자체가 한 데이터에대해 여러개의 컴포넌트가 관여하는 것을 효율적으로 관리하기위함인데, Mutations에 비동기 처리 로직들이 포함된다면, 같은 값에대해 여러개의 컴포넌트에서 변경을 요청했을때 그 변경 순서 파악이 어렵기 때문입니다.

이러한 문제점과 마주치지않기위해 Actions에는 비동기 처리 로직을, Mutations에는 동기 처리 로직으로 나눠서 구현하는 것입니다.

그렇다면, setTimeout()이나 서버와의 http통신처리같은 로직은 Actions에 선언하겠군요!

<h3>
  Actions 등록
</h3>

```
//store.js

export const store = new Vuex.Store({
	//...
	mutations: {
		addCounter: function(state, payload) {
			return state.counter++;
		}
	},
	actions: {
		addCounter: function(context) {
			return context.commit('addCounter');
		}
	}
})
```

actions는 결국 mutations의 메서드를 호출합니다.

```
//App.vue
methods: {
	addCounter() {
		this.$store.dispatch('addCounter');
	}
}
```
