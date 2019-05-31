<h1>
    Primitive vs Reference
</h1>

원시값과 참조값

```
원시값
Boolean
Number
String
Null
Undefined

참조값
Object	
```

```
원시 타입 변수 복사
var x = 100;
var y = x;
x = 99;
y;	// 100
```

```
참조 타입 변수 복사
var x = {count : 100};
var y = x;
x.count = 99;
y.count;	//99
```

위의 예제들처럼 원시값은 value를 넘겨주고, 참조값은 변수의 값이 저장된 힙(Heap) 메모리의 주소값을 저장합니다.

다시한번 예제를 보겠습니다.

```
var a = {
    name : "junwoo",
    message : "hello"
}
var b = a;
b.message = "good night";

console.log(a);
//{
//    name : "junwoo",
//    message : "good night"
//}

console.log(b)
//{
//    name : "junwoo",
//    message : "good night"
//}
```

변수 a는 초기화시 Heap 메모리에 생성된 객체의 메모리 주소를 저장합니다.

그리고 var b = a에서, 변수 a 초기화시 생성된 객체를 변수b에 복사하는게 아니라, a가 가진 메모리 주소, 즉 그 객체를 가리키는 메모리 주소를 복사하는 것입니다.

따라서 변수 a와 b는 둘다 같은 메모리 위치를 가리키게 됩니다.

같은 객체를 가리키는 것이므로, 변수a에 적용되는 변화는 변수b에게도 적용되게됩니다.



아래의 예시처럼 함수에 argument를 넘겨줄 때에도 헷갈릴 수 있습니다.

```
function test(a, b){
    a = 10;
    b.name = "hello world"
}

var a = 500;
var b = {
    name : "good day"
}

test(a, b);

console.log(a);	// 500
console.log(b);	// "hello world"
```



