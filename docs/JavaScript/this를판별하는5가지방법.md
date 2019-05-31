this



자바스크립트를 공부할 때 this는 참 헷갈립니다.



비둘기 : "나는 배가 고프다."

갈매기 : "나는 새우깡이 좋아."

독수리 : "나는 날고 싶어."



자바스크립트의 this는 "나"와 비슷합니다.

문맥에 따라서 가리키는 대상이 다르죠.



헷갈리는 this를 좀 더 쉽게 이해하기위해서 

this를 파악하기위한 5가지 공식을 준비해봤습니다.



1. 암시적 바인딩
2. 명시적 바인딩
3. new 바인딩
4. 윈도우 바인딩
5. strict모드



1.암시적바인딩

첫번째 공식은, 함수가 실행될 때, " . "앞의 녀석이 this가 된다는 것입니다.

```
const person = {
    name : "junwoo",
    age : 100,
    greet() {
        console.log(`hello! my name is ${this.name}`);
    }
}

person.greet();	// "hello! my name is junwoo"
```

person.greet()의 " . " 앞의 단어는 person입니다.

this.name은 이 경우에는 person.name인거죠.

```
greet() {
    // console.log(`hello! my name is ${this.name}`);
    console.log(`hello! my name is ${user.name}`);
}

이렇게 실행되는것과 마찬가지입니다.
```



다음은 조금 더 어려운 경우입니다.

```
const person = {
    name : "junwoo",
    age : 100,
    greet() {
        console.log(`hello! my name is ${this.name}`);
    },
    mother : {
        name : "jin",
        greet() {
            console.log(`hello! my name is ${this.name}`);
        }
    }
}

person.greet();
person.mother.greet();
```

이런 경우에는 무엇이 출력될까요?

함수가 실행될때, " . " 앞에 있는 녀석이 this라고 했습니다.

이 경우에도 똑같이 적용하면 됩니다.

```
person.greet();	// "hello! my name is junwoo"
person.mother.greet();	//"hello! my name is jin"
```



2.명시적바인딩(call, apply, bind)

this와 더불어 자바스크립트를 공부하는 우리들을 괴롭히는 call, apply, bind입니다.

두번째 공식입니다.

call,apply,bind의 경우는 바로 뒤에 나오는 괄호 안에 들어있는 첫번째 단어가 this입니다.

```
function greet() {
    console.log(`hello, my name is ${this.name}`);
}

const user = {
    name : "junwoo",
    age : 100
}

greet.call(user);	// "hello, my name is junwoo"
```

greet.call(user)은 call 뒤의 괄호 안에 user가 this 겠죠?



3. new 바인딩

new는 뒤에 함수이름이 따라온답니다.

```
function Person(name, age) {
    this.name = name;
    this.age = age;
}

const me = new Person("junwoo", 100);
```

이런식으로 new 뒤에는 Person이라는 함수가 오게됩니다.

세번째 공식입니다.

new 바인딩은 this가 빈 객체를 가리킵니다. 



천천히 설명해보겠습니다.

```
let obj = {};

obj.name = "junwoo";

console.log(obj);	//{name : "junwoo"}
```

obj라는 변수에 빈 객체를 할당했습니다.

그리고 obj의 name이라는 key값에 "junwoo"라는 value를 넣어줬구요.

obj를 출력하면 {name : "junwoo"}가 출력됩니다.



이러한 방법과 똑같습니다.

```
function Person(name, age) {
    this.name = name;
    this.age = age;
}

const me = new Person("junwoo", 100);
```

new 연산자는 빈 객체를 만들어냅니다.

그리고 this는 이 빈 객체를 가리키고요.

위의 예시는 다음과 같습니다.



```
function Person(name, age) {
	//this.name = name;
    {}.name = name;
    //this.age = age;
    {}.age = age;
}

const me = new Person("junwoo", 100);
```

빈 객체의 name이라는 key값에 인자로 들어오는 name을 할당해줍니다.

빈 객체의 age라는 key값에 인자로 들어오는 age를 할당해줍니다.

"junwoo"와 100이 각각 들어가겠네요.

console.log(me)를 해보시면

{name : "junwoo", age : 100}이 출력됩니다.



4. 윈도우 바인딩

네번째 공식입니다.

함수로 실행되었을때, this는 window입니다.

```
function person() {
    console.log(`hello! my name is ${this.name}`);
}

const user = {
    name : "junwoo",
    age : 100
}

person();	//"hello! my name is undefined"
```



첫번째 규칙과 헷갈릴 수 있습니다.

첫번째 규칙은 함수가 실행될 때 " . " 앞의 녀석이 this이다! 였죠?

지금은 앞에 " . "이 없이 함수가 실행되고 있는겁니다.

또한 call, apply, bind도 사용하지 않고있구요. 

new도 사용하지 않고있습니다.

```
window.name = "bada";

function person() {
    console.log(`hello! my name is ${this.name}`);
}

person();	// "hello! my name is bada"
```



5. strict모드

마지막 다섯번째 공식입니다.

strict모드에서 this는 undefined입니다.

```
'use strict'

window.name = "bada";

function person() {
    console.log(`hello! my name is ${this.name}`);
}

person();	// Uncaught TypeError: Cannot read property 'name' of undefined
```

4번 예시와 똑같지만 다른점 하나는 'use strict'를 사용해서 엄격모드를 실행했다는 점입니다.

strict모드를 사용한다면 this는 undefined입니다.



this를 판별하는 방법을 정리해보겠습니다.

1. 함수가 어디서 실행되고있는지 확인한다.

2. 함수 앞에 " . "이 있나!? 

   있으면 " . "앞에 있는 참조가 this!

3. 함수가 call, apply, bind로 실행되고 있나!?

   있으면 괄호 안에 들어있는 참조가 this!

4. 함수가 new 키워드로 실행되고 있나!?

   그렇다면 this는 빈 객체!

5. 엄격모드를 사용중인가?

   그렇다면 this는 undefined!

6. 이 모든 경우가 아니라면 this는 window!





참고자료 : https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/



