# 자바스크립트의 객체

- 클래스 없이도 객체를 생성할 수 있음
- ECMAScript을 따르는 언어중 하나
- 키-값의 쌍으로 이루어진 일종의 해시 테이블
  - 키: String, Symbol 타입만 사용 가능
  - 값: 모든 언어 타입 사용 가능

## 객체 생성

- 자바스크립트에서의 객체는 모두 Object 타입의 인스턴스이다.
- 빈 객체라도 Object의 인스턴스 메서드를 사용할 수 있다. (프로토타입으로 인한 상속)

```js
var obj = {};
// var obj = new Object();

obj.hasOwnProperty(key); // 해당 프로퍼티가 상속받지 않은 객체 고유한 프로퍼티인지
obj.toString(); // 스트링으로 형변환할때 호출
obj.valueOf(); // 숫자로 형변환 할때 호출
```

## 객체 리터럴

- 기본 객체를 생성하는 숏컷
- 객체를 이용해 데이터를 표현할때 자주 사용
- JSON 문법의 기반
  - JSON은 프라퍼티 명에 반드시 쌍따옴표("")를 사용
  - JSON은 오직 string, number, array, true, false, null만 값으로 사용 가능

```js
var person = {
  name: 'Tom',
  age: 20,
  hobby: 'Programming',
  sayHi: function() {
    alert('hi');
  }
};
```

## 객체 접근

- 자바스크립트는 이미 만들어진 객체에 프로퍼티를 추가하거나 삭제하는 행위가 자유롭다.
- 닷노테이션이나 배열의 인덱스형태로 프로퍼티에 접근가능

## 객체 접근 - 프로퍼티 추가

```js
var obj = {
  gender: 'male',
  email: 'xx@xx.com'
};

obj.name = 'aa'; //프로퍼티가 없으면 프로퍼티 추가
obj.name = 'bb'; //프로퍼티가 있으면 값변경
obj.getName = function() {};

// 대괄호를 이용해 배열의 인덱스 형태로도 접근 가능
obj['name'] === 'bb';

// 유효한 식별자가 아닌 경우 항상 [] 을 사용
obj.1st // error
obj['1st'] = 'first';

var propName = 'age';
obj[propName] = 10; //obj.age = 10;
obj['my' + propName] = 10; //obj.myage = 10;
```

## 객체 접근 - 프로퍼티 삭제

```js
var obj2 = {
  name: 'Tom'
}

// null 값을 대입해도 프로퍼티는 지워진게 아니다.
obj2.name = null;
('name' in obj2) === true;

// delete으로 완전히 삭제
delete obj2.name; //정상적으로 지워지면 true 리턴

obj2.name === undefined;
('name' in obj2) === false;
```

## 객체 접근 - 객체 삭제

- 개체로의 참조는 끊을수 있어도 객체를 직접 삭제할순 없다.
- 어떤것에도 참조되지 않는 객체는 GC에 의해 언젠가 소멸

```js
var foo = {};

foo = null; // foo가 참조하던 객체의 참조가 끊김

// 언젠가 GC에 의해 객체가 메모리 상에서 소멸됨
```

## 실습(1) :PRACTICE:

- 객체 리터럴을 이용해 Todo객체를 만들어보자
  - index.html과 index.js파일을 만든다.
- 프로퍼티
  - 데이터
    - complete: 완료, 미완료 여부, 기본값 false
    - title: 할일 내용, 기본값 "" 빈 스트링
  - 메소드
    - getTitle: 컨텍스트의 내용을 리턴한다, 빈 함수
    - setComplete: 완료, 미완료 처리, 빈함수

## 실습(1) - Example :EXAMPLE:

```js
var todo = {
  complete: false,
  title: "",
  getTitle: function() {},
  setComplete: function(complete) {}
};
```

# Object.defineProperty()

## Object.defineProperty()

- 객체의 프로퍼티에 특별한 속성을 적용
- 속성으로 프로퍼티의 접근 권한을 설정
- 프로퍼티 getter, setter를 만들 수 있다.
- ES5 스펙(정상적인 사용은 IE9부터 사용가능)
  - IE8도 가능은 한데 DOM객체에만 적용 가능

```js
var obj = {};

//마지막 객체로 프로퍼티에 속성을 정의
Object.defineProperty(obj, 'name', {
  value: 'foo',
  configurable: true,
  writable: false
});
```

## Object.defineProperty() - 프로퍼티의 속성

```js
var obj = {};

Object.defineProperty(obj, 'name', {
  value: 'ppap', // 값
  configurable: true, // 삭제, 속성 변경
  writable: true, // 값 변경
  enumarable: true // for-in 루프에서 해당 프로퍼티를 반환
}); // 옵션의 속성을 생략하면 디폴트로 false.

obj.name = 'myValue' // 기본 문법의 프로퍼티 추가는 configurable, writable, enumerable 모두 true
```

## Object.defineProperty() - 사용예(속성) :LIVE:

```js
var obj = {};

//configurable
Object.defineProperty(obj, 'name', {
  configurable: false,
  writable: true,
  enumerable: true,
  value: 'foo'
});

delete obj.name;
obj.name === 'foo'; //삭제불가
//그리고 이후로는 name프로퍼티는 defineProperty로 속성변경 불가

//writable
Object.defineProperty(obj, 'age', {
  writable: false,
  configurable: true,
  enumerable: true,
  value: 37
});

obj.age = 27;
obj.age === 37; //값 변경불가

//enumarable
Object.defineProperty(obj, 'id', {
  enumerable: false,
  configurable: true,
  enumerable: true,
  writable: true,
  value: 'bar'
});

for (var key in obj) {
  console.log(key); // id는 루프안에 포함되지 않음
}
```

## Object.defineProperty() - 사용예(getter, setter) :LIVE:

- getter, setter는 계산형 프로퍼티 만들거나 프로퍼티의 데이터를 외부에 간접적으로 노출할 때 사용한다.
  - 함수형태로 정의한다. 그래서 setter에서 동명의 프로퍼티에 값을 할당하면 무한 루프 생김

```js
var obj = {};
var ageNum = 0;

Object.defineProperty(obj, 'age', {
  set: function(value) {
    ageNum = value;
  },
  get: function() {
    return ageNum + '살';
  }
});


obj.age = 10;

console.log(obj.age); // 10 '살'
```

## 실습(2) :PRACTICE:

- 이전 실습에서 작업한 Todo에 state라는 프로퍼티를 defineProperty로 추가하면서 다음과 같은 getter를 추가한다.
  - complete이 true면 "완료" 를 리턴
  - complete이 false면 "미완료" 를 리턴

## 실습(2) - Example :EXAMPLE:

```js
var todo = {
  complete: false,
  title: "",
  getTitle: function() {},
  setComplete: function(complete) {}
};

Object.defineProperty(todo, 'state', {
  get: function() {
    if (this.complete) {
      return '완료';
    } else {
      return '미완료';
    }
  }
});
```

# this

- this는 객체의 메소드에서 현 인스턴스 컨텍스트에 접근할때 사용하는 키워드
- 자바스크립트에서는 상황에 따라 this가 참조하는 대상이 달라짐
- 함수가 실행되기 전에 this의 내용이 결정됨

## 글로벌 컨텍스트에서의 this

- 글로벌 컨텍스트: 어떤 함수에도 속하지 않은 함수 밖의 공간
- this `=` window 객체
- 글로벌 컨텍스트에서 변수나 함수가 정의되면 window객체에 속하게됨
- 글로벌 컨텍스트에서 this를 사용하는 경우는 거의 없다.

```js
//세가지의 작업은 동일한 결과
var a = 10;
this.a = 10;
window.a = 10;
```

## 메서드안에서의 this(1)

- 메서드: 실행될때 객체와 연결되서 실행되는 함수
- this는 메서드가 정의될때가 아닌 실행될때 결정(함수를 실행하기 전에 엔진에서 준비해줌, 실행 컨텍스트에 포함)
- this `=` 메서드를 실행할때 연결된 객체

```js
todo.getTitle(); //getTitle안에서의 this는 todo
```

## 메서드안에서의 this(2)

- 같은 함수라도 다른 객체와 연결되어 실행되면 this가 변경됨

```js
nottodo.getTitle = todo.getTitle;
nottodo.getTitle();
```

- nottodo안에 getTitle 메서드가 필요로하는 프로퍼티가 없다면 에러발생

## 함수안에서의 this

- 메서드와 달리 실행할때 연결된 객체가 없다.
- window객체의 메서드로 간주한다.
- this `=` window
- strict mode에서는 undefined

```js
var getTitle = todo.getTitle;
getTitle();
window.getTitle();
```

## 이벤트 리스너 안에서의 this

- DOM 이벤트 리스너 안에서 this는 이벤트가 적용되는 엘리먼트

```js
var element = document.getElementById('myButton');

element.addEventListener('click', function() {
  this === element; //this는 element변수가 참조하는 엘리먼트 객체
}, false);
```

## 실습(3) :PRACTICE:

- 이전에 작성한 todo객체에서 메서드들이 정상적으로 동작하게 해보자
- getTitle()는 title 프로퍼티를 리턴
- setComplete()은 불린값을 인자로 하나 받아서 complete값을 변경

## 실습(3) - Example :EXAMPLE:

```js
var todo = {
  complete: false,
  title: "",
  getTitle: function() {
    return this.title;
  },
  setComplete: function(complete) {
    this.complete = complete;
  }
};
```

# this의 변조

- 자스의 함수는 Function 타입의 인스턴스 so 인스턴스 메서드 사용 가능(Callable Object)
- 함수를 실행할때 this를 임의로 정해서 실행 -> call(), apply()
- 함수의 this가 변경되지 않도록 고정 -> bind()

## Call, Apply - 1

```js
var todo = {
  complete: false,
  title: "자바스크립트 공부하기"
}

function setComplete(complete) {
  this.complete = complete;
}

setComplete(true);

window.complete === true;
```

- todo객체와 setCompete함수는 아무 관계가 없다.
- setComplete을 그냥 실행하게 되면 글로벌 컨텍스트에 complete 프로퍼티가 생성
- strict mode에서는 에러발생
- setComplete함수가 todo객체의 값을 바꾸게 하고 싶다.

## Call, Apply - 2

- call이나 apply메서드를 이용해 관계를 만들어줄 수 있다.
- 함수안의 this를 원하는 객체를 선택해서 실행한다.

```js
var todo = {
  complete: false,
  title: "자바스크립트 공부하기"
}

function setComplete(complete) {
  this.complete = complete;
}

// call: 첫번째 인자 this로 만들 객체, 두번째 인자부터 함수에 전달할 인자
setComplete.call(todo, true);
// apply: 첫번째 인자 this로 만들 객체, 두번째 인자에 함수에 전달할 인자들을 배열로
setComplete.apply(todo, [true]);

todo.complete === true;
```

## Bind

- ES5 스펙
- this가 특정 객체로 고정된 함수를 리턴

```js
var todo = {
  complete: false,
  title: "자바스크립트 공부하기"
}

function setComplete(complete) {
  this.complete = complete;
}

var setCompleteOfTodo = setComplete.bind(todo);

setCompleteOfTodo(true);

todo.complete === true;
```

- setCompleteOfTodo의 this는 이제 절대로 안바뀜
  - 다른 객체 안에서 메소드로 실행할때도
  - apply, call과 실행해도

## 실습(4) :PRACTICE:

1. this의 complete값에 따라 아래와 같이 console.log메세지를 출력하는 함수 printTodo() 구현
   - complete `=` true ? "[완료] title 프로퍼티 내용"
   - complete `=` false ? "[미완료] title 프로퍼티 내용"
2. call과 bind를 이용해서 각 한번씩 this를 todo로 변경해서 실행한다.

```js
var todo = {
  complete: false,
  title: '자바스크립트 공부하기'
};

function printTodo() {
  //직접 코드 구현
}

// 1) call이용해서

// 2) bind를 이용해서
```

## 실습(4) - Example :EXAMPLE:

```js
var todo = {
  complete: false,
  title: '자바스크립트 공부하기'
};

function printTodo() {
  if (this.complete) {
    console.log("[완료] " + this.title);
  } else {
    console.log("[미완료] " + this.title);
  }
}

// 1) call이용해서
printTodo.call(todo);

// 2) bind를 이용해서
var newPrintTodo = printTodo.bind(todo);
newPrintTodo();
```

## 실습(5) :PRACTICE:

- call메서드를 이용해 bind함수를 직접 구현해 본다.
- hint: 함수는 함수를 리턴할 수 있다.(클로저)

```js
var person = {
  name: 'Steve Jobs'
}

function printPersonName() {
  console.log(this.name);
}


function myBind(func, context) {
  return function() {
    //여기를 구현
  }
}

var printPersonNameBinded = myBind(printPersonName, person);

printPersonNameBinded(); // "Steve Jobs"
```

## 실습(5) - Example :EXAMPLE:

```js
var person = {
  name: 'Steve Jobs'
}

function printPersonName() {
  console.log(this.name);
}


function myBind(func, context) {
  return function() {
    func.call(context);
  };
}

var printPersonNameBinded = myBind(printPersonName, person);

printPersonNameBinded(); // "Steve Jobs"
```

# 객체 생성 패턴

## 팩터리 함수

- 리터럴은 객체를 여러개 생성할때 부적합함.
- 팩터리 패턴: 객체의 생성 과정을 캡슐화.
- 원하는 객체를 만드는 함수를 작성해 여러개의 객체를 만들 수 있게 함.

```js
var person = {
  name: 'Steve Jobs'
};

function createPerson(name) {
  var newPerson = {};

  newPerson.name = name;

  return newPerson;
};

var person2 = createPerson('Steve Jobs');
var person3 = createPerson('Bill Gates');
```

## 실습(6) :PRACTICE:

- 타이틀의 내용을 인자로 전달받아서 todo 객체를 만드는 createTodo함수를 만들어보자
- 객체의 프로퍼티는 닷노테이션을 이용해 한개씩 추가한다.(한번에 리터럴로 리턴 금지)
  - [obj.name](http://obj.name/) = 'foo'; // 이렇게요 :)

```js
function createTodo(title) {
  // 완성하셔요 :)
}

var todo1 = createTodo('출근하기');
var todo2 = createTodo('퇴근하기');

todo1.getTitle() === '출근하기';
todo2.getTitle() === '퇴근하기';
```

## 실습(6) - Example :EXAMPLE:

```js
function createTodo(title) {
  var todo = {};

  todo.complete = false;

  todo.title = title;

  todo.getTitle = function() {
    return this.title;
  };

  todo.setComplete = function(complete) {
    this.complete = complete;
  };

  return todo;
}

var todo = createTodo('자바스크립트 배우기');
```

## 생성자

- 자스에서 클래스의 역할을 한다.
- 객체의 생성뿐 아니라 만들어지는 객체는 생성자의 타입으로 구분될수 있다.
- 일반 함수를 new 키워드와 함께 실행하면 생성자로 동작
- new 키워드로 인해 this가 새로운 객체를 가르킨다.

```js
function Person(name) {
  this.name = name;
}

var person = new Person('Steve Job');
```

## new 연산자로 인한 내부 동작(1)

```js
// new없이 실행하면
var person = Person('Steve Job');

function Person(name) {
  this = window //1. 객체와 실행된게 아니니 this는 window

  this.name = name; //2. 함수의 코드를 실행

  return undefined //3. 모든 함수는 리턴값이 없으면 undefined 리턴
}
```

## new 연산자로 인한 내부 동작(2)

```js
var person = new Person('Steve Job');

// new와 사용했을때 함수 내부 동작
function Person(name) {
  //1. 새로운 객체를 만든다.
  this = {};

  //2. 객체와 생성자의 프로토타입을 연결한다.(이 부분 생략)

  //3. 함수(생성자)의 코드를 실행
  this.name = name;

  //4. 만들어진 객체를 리턴한다.
  return this;
}
```

## 객체 타입 비교

- 생성자를 이용해 객체를 생성하면 생성자의 타입을 가질수 있다.
- 타입 판단은 `constructor` 와 `instanceof` 연산자를 이용할 수 있다.
- `typeof` 키워드로 타입을 확인할 수 있지만 기본 언어 타입만 구분됨(모든 객체는 'object' 타입으로 판단)

```js
function Human() {};

var man = new Human();

typeof man // 'object'
man.constructor === Human; // true
man instanceof Human // true
```

## 실습(7) :PRACTICE:

- 팩터리 패턴으로 만들어진 createTodo함수를 생성자로 만들어보자
- 생성자명은 Todo();

## 실습(7) - Example :EXAMPLE:

```js
function Todo(title) {
  this.complete = false;

  this.title = title;

  this.getTitle = function() {
    return this.title;
  };

  this.setComplete = function(complete) {
    this.complete = complete;
  };
}

var todo = new Todo('자바스크립트 배우기');
```

# 프로토타입

## 생성자만 사용했을때의 문제

- 생성자가 만들어낸 객체들의 메소드들은 메모리상에 중복해서 생성된다.

```js
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;

  this.getFullName = function() {
    return this.firstName + this.lastName;
  };
}

var P1 = new Person('John', 'Doe');
var P2 = new Person('Robert', 'Doe');

P1.getFullName !== P2.getFullName; //기능적으로 동일하지만 같은 인스턴스가 아님, 낭비
```

## 프로토타입의 아이디어

```js
//프로토타입의 기본적인 아이디어

//생성자에서는 객체 별로 고유한 데이터에 해당되는 프로퍼티들만 만듬
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

//객체끼리 공통적인 메소드들은 따로 정의해서 공용으로 사용
var personMethods =  {
  getFullName: function() {
    return this.firstName + this.lastName;
  }
};
```

## 프로토타입의 적용

- 생성자의 prototype 프로퍼티 객체에 공용 메서드들을 추가.

```js
//생성자에서는 객체 별로 고유한 데이터에 해당되는 프로퍼티들만 만듬
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

// prototype에 공용 메서드들을 선언한다.
// prototype 프로퍼티는 함수 타입의 인스턴스 프로퍼티로 초기 값은 빈 객체
Person.prototype.getFullName = function() {
  return this.firstName + this.lastName;
}

var P1 = new Person('John', 'Doe');
var P2 = new Person('Robert', 'Doe');

P1.getFullName === P2.getFullName;
//프로토타입의 getFullName을 공유함으로 물리적으로 동일한 메서드
```

## 프로토타입 위임의 동작 원리

```js
var p1 = new Person('John', 'Doe');

// (new키워드로 인한 엔진의 내부 작업)
p1.__proto__ = Person.prototype; // 인스턴스마다 Person.prototype으로 향하는 포인터를 만듬

//프로토타입에 있는 메서드 실행
p1.getFullName();
```

![프로토타입 동작원리](https://nhnent.dooray.com/files/1978306210282451012)

1. 현재 객체(p1)에서 getFullName메서드를 찾음 -> (없다)
2. 못찾았으면 현재객체(p1)의 __proto__프로퍼티가 가르키는 객체로 이동(Person.prototype)
3. Person.prototype 에서 getFullName메서드를 찾아서 실행

## 프로토타입의 특징(1)

- 프로토타입의 내용을 동적으로 변경하면 미리 생성된 객체에도 적용된다.

```js
// 미리 객체를 생성하고
var p1 = new Person('John', 'Doe');

// 프로토타입에 메서드를 추가해도
Person.prototype.addedMethod = function() {};

//정상 실행
p1.addedMethod();
```

- constructor 프로퍼티를 이용해 프로토타입이 사용되는 생성자를 알 수 있다.(타입체크를 위해 사용)

```js
p1.constructor === Person; // Person.prototype.constructor === Person
```

## 프로토타입의 특징(2)

- 객체 인스턴스에서는 프로토타입의 내용을 읽을수는 있지만 쓸수는 없다.
- 그리고 이점을 이용해 상속 구조에서 메서드 오버라이드를 구현한다.

```js
function Person() { ... }
Person.prototype.getFullName = function() {...}

var p1 = new Person('John', 'Doe');

p1.getFullName = function() {};
//p1객체에 새로운 getFullName메서드가 생길뿐 prototype의 내용은 안바뀜
```

## 실습(8) :PRACTICE:

- Todo를 프로토타입을 이용해 정의한다.

```js
function Todo(title) {
  // 작성해주세요 :)
}

Todo.prototype // Todo.prototype을 확장해주세요 :)
```

## 실습(8) - Example :EXAMPLE:

```js
function Todo(title) {
  this.complete = false;
  this.title = title;
}

Todo.prototype.getTitle = function() {
  return this.title;
};

Todo.prototype.setComplete = function(complete) {
  this.complete = complete;
};
```

# 상속

## Prototypal 상속(1)

- 클래스기반 언어에서는 서브클래스로 속성이나 메서드를 상속해준다.(위에서 아래로 내려줌)
- 자스에서는 상속이라기 보다는 자신에게 없는 메서드나 속성을 다른 객체로 위임해서 사용하는 개념이다.(아래에서 위로 올라감)
  - 사실 위아래도 없다. 그냥 위임 대상일뿐
- 자스에서의 상속(위임)은 객체가 상속(위임)받을 객체를 `[[prototype]]` 라는 스펙상의 내부 속성(internal slot)으로 연결하는것으로 구현된다.
- 표준 스펙은 이니지만 브라우저 벤더들이 `[[protoype]]` 내부 속성을 객체안의 `__proto__` 라는 프로퍼티로 노출해 자스 코드로 접근은 가능
- 다중상속(다중 위임) 불가능
- 프로토타입 위임의 끝은 항상 Object.prototype

## Prototypal 상속(2)

- 객체 리터럴이나 Object생성자로 인스턴스를 생성하면 `__proto__` 프로퍼티는 `Object.prototype` 를 가르킨다.(참조값을 갖는다)
- 객체 리터럴이나 생성자로 만들어진 인스턴스는 `Object.prototype` 객체의 메서드를 마치 직접 소유한것처럼 위임해 사용할 수 있다.

```js
// 리터럴로 생성
var i = {}; // i.__proto__ === Object.prototype

// 생성자로 생성
var i = new Object(); // i.__proto__ === Object.prototype
```

## Prototypal 상속(3)

```js
var a = {
  pMethod: function() {}
};

var b = {
  cMethod: function() {}
};

a.__proto__ === Object.prototype // true
b.__proto__ === Object.prototype // true
```

- `b` 객체가 프로토타입 위임을 통해 `a` 의 메서드에 접근할 수 있게 만들어 보자.

## Prototypal 상속(4)

- b의 `__proto__` 프로퍼티의 값을 a객체로 덮어쓴다.

```js
var a = {
  pMethod: function() {}
};

var b = {
  __proto__: a,
  cMethod: function() {}
};
```

## Prototypal 상속(5)

- 상속 구조로 본다면 `a` 는 parent 그리고 `b` 는 child 라고 할 수 있다.

```js
var parent = {
  pMethod: function() {}
};

var child = {
  __proto__: parent,
  cMethod: function() {}
};
```

## Prototypal 상속(6) :LIVE:

grandChild 도 같은 방법으로 만들 수 있다.

```js
var parent = {
  pMethod: function() {}
};

var child = {
  __proto__: parent,
  cMethod: function() {}
};

var grandChild = {
  __proto__: child,
  gcMethod: function() {}
};
```

## Prototypal 상속(7)

- `__proto__` 는 표준이 아니다.
- 객체와 객체의 프로토타입 연결은 표준 API Object.create() 스태틱 메서드를 사용
  - 새로운 객체를 만들고 `__proto__` 프로퍼티를 `Object.create()` 의 인자로 전달된 객체와 연결한뒤 리턴

```js
var parent = {
  pMethod: function() {}
};

var child = Object.create(parent); // child.__proto__ --> parent

child.cMethod = function() {}
```

## 실습(9) Object.create :PRACTICE:

- Object.create 을 이용해 아래와 같은 위임 구조의 객체들을 생성한다.
  - grandChild -> child -> parent
- parent에 메서드를 추가하고 해당 메서드를 grandChild에서 호출 가능한지 확인한다.

## 실습(9) Object.create :EXAMPLE:

```js
var parent = {};

var child = Object.create(parent); 
var grandChild = Object.create(child);
```

## 생성자 기반 프로토타입 체인 상속(1)

- 자바스크립트의 상속은 객체만으로도 가능하지만 객체간의 관계로 어플리케이션을 디자인하기에는 무리가 있다.
- 그래서 클래스와 비슷한 역할을 하는 생성자를 도입하게 되었다.
- 생성자는 원하는 프로토타입 체인 구조의 객체를 찍어내기 위한 도구
  - 프로토타입 체인은 링크드 리스트 형태로 연결된 객체 위임 구조

## 생성자 기반 프로토타입 체인 상속(2)

- 원하는 모습의 프로토타입 체인을 가진 객체를 만들어 내는 생성자를 만들어보자.
- Child 타입이 Parent 타입을 상속 받도록 만든다.

```js
function Parent() {}
function Child() {}

var p2 = new Child();
```

- 자스의 상속의 의미
  1. Child 타입의 인스턴스는 Parent 생성자의 prototype 객체에 접근 할 수 있어야한다.
  2. Child 타입의 인스턴스는 Parent 생성자가 만드는 인스턴스 별로 고유해야할 속성을 동일하게 갖는다.

## 생성자 기반 프로토타입 체인 상속(3)

- 프로토타입 체인 연결

```js
function Parent() {}
function Child() {}

var p1 = new Parent();
var p2 = new Child();
```

- p1, p2는 서로 다른 프로토타입 체인을 갖고있다.

![프로토타입체인상속3](https://nhnent.dooray.com/files/1870018215055324799)

## 생성자 기반 프로토타입 체인 상속(4)

- 생성자의 상속 구조는 생성자의 프로토타입 객체들을 프로토타입 체인으로 연결하는것으로 만들어진다.
- Child 타입이 Parent 타입을 상속받으려면
  - Child 생성자의 프로토타입 객체가 `__proto__` 로 Parent 생성자의 프로토타입 객체와 연결되면 된다.

![프로토타입체인상속4](https://nhnent.dooray.com/files/1981806134528023533)

## 생성자 기반 프로토타입 체인 상속(5) :LIVE:

- Parent 생성자의 prototype 객체를 상속받는 Child 타입 구조

```js
function Parent() {}
Parent.prototype.pMethod = function() {};

function Child() {}
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;
Child.prototype.cMethod = function() {};

var p2 = new Child(); //p2.__proto__ === Child.prototype
```

## 실습(10) :PRACTICE:

- 각 생성자 GrandChild -> Child-> Parent로 이어지는 프로토타입 체인 상속 구현
- 각각 타입의 프로토타입에 메소드 한개 이상 정의

## 실습(10) - Example :EXAMPLE: :LIVE:

```js
function Parent() {}
Parent.prototype.pMethod = function() {};

function Child() {}
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;
Child.prototype.cMethod = function() {};

function GrandChild() {}
GrandChild.prototype = Object.create(Child.prototype);
GrandChild.prototype.constructor = GrandChild;
GrandChild.prototype.cMethod = function() {};
```

## 부모 생성자의 인스턴스 속성 상속 :LIVE

- 프로토타입에서는 공용으로 사용할 메서드를 정의하고 생성자 함수 안에서는 인스턴스 별로 고유해야할 속성을 정의한다.
- 프로토타입 체인으로 부모들의 프로토타입의 내용은 상속받아도 부모 생성자가 만드는 인스턴스 프로퍼티는 상속 받을 수 없다.

```js
function Parent(name) {
  this.name = name;
}

function Child() {}
Child.prototype = Object.create(Parent.prototype);

// 생성자 빌려쓰기 시전
function Child(name) {
  Parent.call(this, name);
}

var i = new Child('lime');
```

## 메서드 오버라이드

- 메서드 오버라이드: 상속받은 메서드를 재정의
- 체인에선 실행 객체와 제일 가까운 메서드가 우선 순위가 높다.
- 제일 우선순위가 높은건 객체 안에 있는 메서드

```js
function Parent() {}
Parent.prototype.getName = function() {
  return 'parentName';
}

function Child() {}
Child.prototype.getName = function() {
  return 'childName';
}

//... 상속과정 생략 프로토타입 체인은 p2 -> Child.prototype -> Parent.prototype

var p2 = new Child();

p2.getName(); // 'childName'

p2.getName = function() {
  return 'p2Name';
}

p2.getName() // 'p2Name';
```

## 실습(11) :PRACTICE:

- Todo에 getDisplayText()메서드 추가
  - this의 complete값에 따라 아래와 같이 스트링 리턴
    - complete `=` true ? "[완료] title 프로퍼티 내용"
    - comptete `=` false ? "[미완료] title 프로퍼티 내용"
- Todo에 print() 메서드 추가
  - getDisplayText()의 내용을 console.log()로 출력해 주는 메서드
- Todo를 상속받아 아래와 두개의 하위 타입을 만든다.
  - OfficeTodo, HomeTodo
- OfficeTodo, HomeTodo에서 getDisplayText 메서드를 오버라이드 구현한다.
  - "-Office- [완료] title 내용"
  - "-Home- [완료] title 내용"
  - Todo의 getDisplayText를 이용해서 구현
    - hint: Todo.prototype.getDisplayText.call();

## 실습(11) - Example :EXAMPLE:

```js
function Todo(title) {
  this.complete = false;
  this.title = title;
}

Todo.prototype.getTitle = function() {
  return this.title;
};

Todo.prototype.setComplete = function(complete) {
  this.complete = complete;
};

Todo.prototype.print = function() {
  console.log(this.getDisplayText());
}

Todo.prototype.getDisplayText = function() {
  if (this.complete) {
    return "[완료] " + this.getTitle();
  } else {
    return "[미완료] " + this.getTitle();
  }
}

function OfficeTodo(title) {
  Todo.call(this, title);
}

OfficeTodo.prototype = Object.create(Todo.prototype);
OfficeTodo.prototype.constructor = OfficeTodo;

OfficeTodo.prototype.getDisplayText = function() {
  return "-Office- " + Todo.prototype.getDisplayText.call(this);
}
```

# class 키워드 사용

## ES6 Class

- 프로토타입과 생성자를 이용한 패턴을 쉽게 사용할 수 있도록 하는 편의 문법
- 내부적으로는 지금까지 설명했던 내용과 동일하게 동작

## 기본 문법

```js
class Person {
  // 생성자
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  // 메소드
  getFullName() {
    return this.firstName + this.lastName;
  }
}
```

## 상속

```js
class Parent {
  constructor(name) {
    this.name = name;
  }
  getName() {
    return this.name;
  }
}

class Child extends Parent {
  // 생략 가능
  constructor(name) {
    super(name);
  }
  getName() {
    return super.getName() + '.Junior';
  }
}
```

## 실습(12) :PRACTICE:

- 실습(10) 에서 진행했던 내용을 class 키워드를 이용해 변경해본다.
- Hint: super.methodName() 을 통해 부모의 메소드를 호출할 수 있다.

```js
class Parent {
  constructor(name) {
    this.name = name;
  }
  getName() {
    return this.name;
  }
}

class Child extends Parent {
  // 생략 가능
  constructor(name) {
    super(name);
  }
  getName() {
    return super.getName() + '.Junior';
  }
}
```

## 실습(12) - Example :EXAMPLE:

```js
class Todo {
  constructor(title) {
    this.complete = false;
    this.title = title;
  }
  getTitle() {
    return this.title;
  }
  setComplete(complete) {
    this.complete = complete;
  }
  print() {
    console.log(this.getDisplayText());
  }
  getDisplayText() {
    if (this.complete) {
      return "[완료] " + this.getTitle();
    } else {
      return "[미완료] " + this.getTitle();
    }
  }
}

class OfficeTodo extends Todo {
  getDisplayText() {
    return "-Office- " + super.getDisplayText();
  }
}

class HomeTodo extends Todo {
  getDisplayText() {
    return "-Home- " + super.getDisplayText();
  }

```