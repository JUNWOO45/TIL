<h1>
  ES6
</h1>

```
항상 const와 let먼저 공부하다가 집중력을 잃고 클래시오브클랜을 하거나 유튜브를 보던 나를 기억하며 Destructuring부터 공부합니다...
역사를 잊은 민족에게 미래는 없댜...퍄.....
```

<hr>

<h2>
  Destructuring
  구조 분해 문법
</h2>



<h3>
  기존 자바스크립트의 '구조'
</h3>



기존 자바스크립트에서 객체와 배열의 구조는 다음과 같습니다.

```
var arr = [1, 2, 3, 4];
var obj = {
	a: 10,
	b: 20,
	c: 30
};
```

왼쪽에는 변수, 오른쪽에는 데이터 타입을 선언합니다.

'구조 분해'란 이러한 변수 선언 방식이 자유로워지는 것을 의미합니다.

```
var { a, b, c } = obj;
```



<h3>
  특정 객체의 값을 꺼내오는 방법
</h3>

```
var person = {
	name: junwoo,
	age: 100,
	area: seoul
};

var name = person.name;
var age = person.age;
var area = person.area;
```

객체의 속성값을 꺼내올때마다 일일이 변수를 하나 생성하고 담아주고 있습니다.

꺼내야할 속성이 많아지면 많아질수록, 새로운 변수를 생성하고 대입하는 식의 반복작업이 계속됩니다.

이러한 상황에서 구조 분해 문법을 적용하면 더 간편하게 꺼내올 수 있습니다.

```
var person = {
	name: 'junwoo',
	age: 100,
	area: 'seoul'
};

var { name, age, area } = person;
console.log(name);
console.log(age);
console.log(area);
```

익숙해져야 합니다!!



<h3>
  뷰엑스에 적용해보기
</h3>

```
사실 아직 뷰엑스를 경험해보지않았지만... 공부해봅니다.
```

구조분해문법을 활용하기 가장 좋은 곳은 뷰엑스의 actions 속성이라고 합니다.

뷰엑스의 actions 속성들은 모두 context라는 인자를 받습니다.

그리고 context의 commit API를 반드시 호출합니다.

```
actions: {
	fetchData(context) {
		context.commit('addProducts');
	}
}
```

구조 분해 문법을 사용하면 다음과같이 바꿀 수 있습니다.

```
actions: {
	fetchData({ commit }) {
		commit('addProducts');
	}
}
```

헷갈리네요...

위 분해 과정을 조금 더 풀어보면,

1. context라는 객체에는 이미 commit속성이 있는 것을 확인했습니다.

   ```
   actions: {
   	fetchData(context) {
   		context.commit('addProducts');
   	}
   }
   ```

2. context객체가 아래와 같이 정의되고 있다고 가정해봅니다.

   ```
   var context = {
   	commit: actionName => console.log(actionName + 'has been committed')
   }
   ```

3. 여기에 구조분해문법을 적용해보면..

   ```
   var { commit } = context;
   commit('addProducts');	// addProducts has been committed
   ```



<hr>

<h2>
  Template Literal
</h2>

알파이자 오메가는 백틱( ` )입니다.

```
const str = `hello es6`;
```

<h3>
  여러 줄에 걸쳐서 문자열 선언하기
</h3>

기존 자바스크립트 string 선언 방식인 따옴표의 문제점은 다음과 같습니다.

```
var str = 'Template literals are string literals allowing embedded expressions. \n' + 
'You can use multi-line strings and string interpolation features with them. \n' + 
'They were called "template strings" in prior editions of the ES2015 specification.';
```

자동으로 개행이 되지않기에, 라인 브레이커인 ' \n'을 개행할 곳마다 추가해주어야했습니다.

문장이 길어지면 길어질수록, + 와 \n은 늘어만 갔습니다..

하지만 백틱을 사용하면 위와같은 방식은 사용하지 않아도 됩니다!

```
const str = `Template literals are string literals allowing embedded expressions.
You can use multi-line strings and string interpolation features with them.
They were called "template strings" in prior editions of the ES2015 specification.`;
```

뷰에서도 자주 적용하는 방법이죠!

```
Vue.component('test-cmp', {
	template: `
		<div>
			<h1>test component</h1>
			<div>back-tick is powerful!</div>
		</div>
	`
})
```



<h3>
  문자열 중간에 변수 바로 대입하기
</h3>

```
const language = 'Javascript';
var expression = `I love ${language}!`;
```

${ }는 위와같이 변수의 대입뿐 아니라, 간단한 연산도 가능합니다.

```
var language = 'Javascript';
var expression = `I love ${language.split('').reverse().join('')}!`;
```



<hr>

<h2>
  Spread Operator
</h2>

스프레드 오퍼레이터는 특정 객체 또는 배열의 값을 다른객체나 배열로 복제하거나 옮길때 사용됩니다.

```
var obj = {
	a: 10,
	b: 20
}

var newObj = {...obj}
```

```
var arr = [1, 2, 3]
var newArr = [...arr]
```

스프레드 오퍼레이터를 이용해서 특정 객체, 배열을 각각 새로운 객체와 배열에 복제했습니다!



<h3>
  기존 자바스크립트의 객체 복제 방식
</h3>

스프레드 오퍼레이터 없을때는..

```
var obj = {
	a: 10,
	b: 20
}

var newObj = {
	a: obj.a,
	b: obj.b
}
```

```
var arr = [1, 2, 3]
var newArr = [arr[0], arr[1], arr[2]]
```

객체를 복사할땐 새로운 객체인 newObj에 새로운 속성들을 선언하고, 각 속성에 obj의 속성들을 일일이 접근해서 대입해줬어야 했습니다.

배열을 복사할땐, 기존 배열 arr의 인덱스에 일일이 접근해서 새로운 요소를 만들어줘야 했습니다.

확실히 스프레드 오퍼레이터의 능력이 돋보입니다.



<h3>
  뷰엑스에 적용해보기
</h3>

뷰엑스의 헬퍼 함수에 잘 활용할 수 있습니다.

```
import { mapGetters } from 'vuex'

export default {
	computed: {
		...mapGetters(['getStrings', 'getNumbers', 'getUsers']),
		anotherCounter() {
			...
		}
	}
}
```

mapGetters라는 헬퍼 함수 앞에 스프레드 오퍼레이터를 사용했습니다.



<h2>
	Enhanced Object Literal
  향샹된 객체 리터럴
</h2>

향샹된 객체 리터럴이란, 기존 자바스크립트에서 사용하던 객체정의방식을 개선한 문법입니다.

기존 자바스크립트 객체 정의 방식은 다음과같습니다.

```
var porson = {
	name: 'junwoo',
	coding: function() {
		console.log('hello world')
	}
}
```



<h3>
  축약문법1 : 속성과 값이 같으면 1개만 기입
</h3>

```
var name = 'junwoo'
var person = {
	name
}

console.log(person)	//{name: 'junwoo'}
```

이러한 축약문법을 뷰 컴포넌트 등록 방식과 뷰 라우터 등록방식에 대입해보면 다음과 같습니다.

```
const myCmp = {
	template: '<p>My Component!</p>'
}

new Vue({
	components: {
		myCmp
	}
})
```

```
const router = new VueRouter({
	...
})

new Vue({
	router
})
```



<h3>
  축약문법2: 속성에 함수를 정의할 때 function 예약어 생략
</h3>

기존에는 객체를 정의할 때 객체의 속성에 함수를 연결하여 사용하는 경우가 많았습니다.

```
const person = {
	coding: function() {
		console.log('hello world')
	}
}

person.coding()	//hello world
```

ES6에서는 다음과 같이 사용합니다.

```
const person = {
	coding() {
		console.log('hello world')
	}
}

person.coding()	//hello world
```

뷰에도 적용해보겠습니다.

```
new Vue({
	...
	methods: {
		fetchData: function() {
			...
		},
		showAlert: function() {
			...
		}
	}
})
```

이러한 뷰 코드를...

```
new Vue({
	methods: {
		fetchData() {
			...
		},
		showAlert() {
			...
		}
	}
})
```



<hr>

<h2>Arrow Function</h2>
```
var a = () => {
	...
}
```

<h3>
  화살표 함수의 다양한 문법
</h3>



<h3>
  1. 단순한 자바스크립트 표현식
</h3>

```
() => 10 + 20;	// {}필요없음.
```



<h3>
  2. 함수 선언 방식
</h3>

```
() => {
	print();
	log();
	return 1 + 2;
}
```



<h3>
  3.전달인자(파라미터)가 하나인 경우
</h3>

```
const a = (num) => { return num + 100 }
const b = num => num + 100

a(10) //110
b(10) //110
```

<hr>



<h2>
  const & let
</h2>

<h3>
  let
</h3>

let 예약어는 한번 선언하면 다시 선언할 수 없습니다.

```
let a = 10;
let a = 20;
//Uncaught SyntaxError: Identifier 'a' has already been declared
```



<h3>
  const
</h3>

const 예약어는 한번 할당한 값을 변경할 수 없습니다.

```
const a = 10;
a = 20;
// Uncaught TypeError: Assignment to constant variable
```

단, 객체나 배열로 선언했을 때 객체의 속성과 배열의 요소를 변경할 수 있습니다.

```
const b = {
	name: 'junwoo',
	age: 100
}

console.log(b.age);	//100

b.age = 200;
console.log(b.age); //200
```

```
const c = [];
console.log(c);	//[]

c.push('good');
console.log(c);	//['good']
```

<h3>
  블록 유효 범위
</h3>

<h3>
  var
</h3>

var의 유효범위는 함수의 블록 단위로 제한됩니다.

함수 스코프(function scope)라고 합니다.

```
var a = 100;
function check() {
	var a = 1;
	console.log(a);
}

check();	// 1
```

check함수 앞에 선언한 a와 check함수 안에 선언한 a는 다른 유효 범위를 갖습니다.

var a = 100은 자바스크립트 전역 객체인 window에 추가가됩니다.

var a = 1은 check함수 안에서만 유효범위를 갖습니다.

<h3>
  for문에서의 var 유효범위
</h3>

```
var a = 10;
for(var a = 0; a < 5; a++) {
	console.log(a);
}
console.log(a);
```

var a = 10으로 변수 a를 선언한 상태에서 for문에 동일한 변수이름 a를 사용해봅니다.

이러면 { }으로 변수의 유효범위가 제한되지않기때문에 for문이 끝나고 나서의 console.log(a)를 출력하면 for문의 마지막 결과값이 출력됩니다.



<h4>
  "이러한 문제점을 해결하고자 const와 let의 변수 유효 범위를 블록{ }으로 제한하였습니다."
</h4>



<h3>
  const와 let
</h3>

```
var a = 10;
for(let a = 0; a < 5; a++) {
	console.log(a);	//0 1 2 3 4
}
console.log(a);	// 10
```

반복문의 조건변수 a를 let으로 선언하여 변수의 유효범위가 for문의 {} 블록 안으로 제한되었습니다.

