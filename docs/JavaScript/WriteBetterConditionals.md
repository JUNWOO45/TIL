

<h1>
  5 Tips to Write Better Conditionals in Javascript
</h1>



<h2>
  1. 여러 조건에 함께 맞아야 할 땐 Array.includes를 사용합니다.
</h2>

```javascript
function test(fruit) {
  if(fruit === 'apple' || fruit ==='strawberry') {
    console.log('Red - !')
  }
}
```

이러한 방법은 괜찮아 보일 수 있지만, apple이나 strawberry말고 또다른 빨간 과일들을 추가해야할 땐 조금 복잡해집니다..

(제가 지금 이런 일할때 문제에 쳐해있죠… includes는 IE에서 전혀 지원하지 않습니다...)

```javascript
function test(fruit) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberry'];
  
  if(redFruits.includes(fruit) {
  	console.log('Red - !');   
  })
}
```



<h2>
  2. 중첩은 최대한 적게, Return은 최대한 빨리!
</h2>

1번의 예시에서 다음 조건들을 추가해보겠습니다.

1) 과일값이 주어지지않는다면 'no fruit'출력.

2) 과일의 갯수가 10개보다 많다면 'big quantity'출력

```javascript
function test(fruit, quantity) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberry'];
  
  //조건1 : 과일값이 존재해야합니다.
  if(fruit) {
    //조건2 : 과일이 빨간색이어야합니다.
    if(redFruits.includes(fruit)) {
    	console.log('Red - !');
      //조건3 : 과일의 갯수가 10개보다 많아야합니다.
    	if(quantity > 10) {
         console.log('big quantity');
      }
    }
  } else {
    throw new Error('no fruit')
  }
}
```

현재는 3단계의 중첩 if문이 존재합니다.

게다가 크게 if-else구문도 있죠.



이걸 다음과같이 **최대한 빨리 return**해봅니다.

```javascript
function test(fruit, quantity) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberry'];
  
  //에러는 최대한 빨리.
  if(!fruit) {
    throw new Error('no fruit');
  }
  if(redFruits.includes(fruit)) {
    console.log('Red - !');
    if(quantity > 10) {
    	 console.log('big quantity');
    }
  }
}
```

이젠 하나의 중첩 if문만 존재합니다.

**조건을 부정하고 최대한 빨리 return함으로써 중첩을 줄이는게 가능해졌습니다.**

한번 더 해보겠습니다.

```javascript
function test(fruit, quantity) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberry'];
 	if(!fruit) {
    throw new Error('no fruit');
  } 
  if(!redFruits.includes(fruit)) {
    return;
  }
  console.log('Red - !');
  if(quantity > 10) {
    console.log('big quantity');
  }
}
```

이제 중첩문이 없어졌네요.

includes조건문을 부정하는하는 방법을 써서 중첩문을 없앴습니다.



<h2>
  디폴트 파라미터와 비구조화문법을 사용합니다.
</h2>

null이나 undefined를 체크하거나 기본값을 설정하기위해 아래처럼 작성했었습니다.

```javascript
function test(fruit, quantity) {
  if(!fruit) {
    return;
  }
  const q = quantity || 1;	//quantity가 주어지지않으면 기본값을 1로 설정
 	console.log(`${q}개의 ${fruit}이 존재합니다!`);
}
```

디폴트 파라미터를 사용한다면, 변수 q를 사용하지 않아도 됩니다!

```javascript
function test(fruite, quantity = 1) {
  if(!fruit) {
    return;
  }
  
  console.log(`${quantity}개의 ${fruit}이 존재합니다!`);
}
```

훨씬 쉽고 직관적입니다.

함수의 모든 파라미터는 기본값을 가질 수 있습니다.

예를 들어, fruit에도 기본값을 주려면..

```javascript
function test(fruit = 'unknown', quantity = 1) {
  ...
}
```

처럼 작성할 수 있습니다.

만약 fruit이 객체라면...

```javascript
function test(fruit) {
  if(fruit && fruit.name) {
    console.log(fruit.name);
  } else {
    console.log('unknown');
  }
}
```





<h2>
  Switch대신에 Map과 Object를 사용합니다.
</h2>

```javascript
function test(color) {
  switch(color) {
    case 'red':
      return ['apple', 'strawberry'];
    case 'yellow':
      return ['banana', 'pineapple'];
    case 'purple':
      return ['grape'];
    default:
      return [];
  }
}
```

이걸 Object를 사용해서 더 간략하게 줄여보겠습니다.

```javascript
const fruitColor = {
  red: ['apple', 'strawberry'],
  yellow: ['banana', 'pineapple'],
  purple: ['grape']
};

function test(color) {
  return fruitColor[color] || [];
}
```

Object대신에 Map을 사용할 수도 있습니다.

```javascript
const fruitColor = new Map()
	.set('red', ['apple', 'strawberry'])
	.set('yellow', ['banana', 'pineapple'])
	.set('purple', ['grape']);

function test(color) {
  return fruitColor.get(color) || [];
}
```

filter를 사용해서도 작성할 수 있습니다!

```javascript
const fruits = [
  {name: 'apple', color: 'red'},
  {name: 'strawberry', color: 'red'},
  {name: 'banana', color: 'yellow'},
  {name: 'pineapple', color: 'yellow'},
  {name: 'grape', color: 'purple'},
];

function test(color) {
  return fruits.filter(f => f.color === color);
}
```



<h2>
  배열의 전체조건에는 Array.every, 부분조건에는 Array.some을 사용합니다.
</h2>

```javascript
const fruits = [
  {name: 'apple', color: 'red'},
  {name: 'banana', color: 'yellow'},
  {name: 'pineapple', color: 'yellow'}
];

function test() {
  let isAllRed = true;
  for(let f of fruits) {
    if(!isAllRed) {
      break;
    }
    isAllRed = (f.color === 'red');
  }
  console.log(isAllRed);	//false
}
```

Array.every를 사용해봅시다.

```javascript
const fruits = [
  {name: 'apple', color: 'red'},
  {name: 'banana', color: 'yellow'},
  {name: 'pineapple', color: 'yellow'}
];

function test() {
  const isAllRed = fruits.every(f => f.color === 'red');
  console.log(isAllRed);
}
```

과일 중 하나라도 빨간색인지를 판별하는 조건문은 다음과 같습니다.

```javascript
const fruits = [
  {name: 'apple', color: 'red'},
  {name: 'banana', color: 'yellow'},
  {name: 'pineapple', color: 'yellow'}
];

function test() {
  const isAnyRed = fruits.some(f => f.color === 'red');
  console.log(isAnyRed);
}
```



---

#### 자료출처

https://ultimatecourses.com/blog/deprecating-the-switch-statement-for-object-literals