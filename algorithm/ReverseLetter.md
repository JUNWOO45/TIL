- 문제

```
Given a string str, reverse it omitting all non-alphabetic characters.

Example
For str = "krishan", the output should be "nahsirk".

For str = "ultr53o?n", the output should be "nortlu".

Input/Output
[input] string str

A string consists of lowercase latin letters, digits and symbols.

[output] a string
```



- 나의풀이

```
function reverseLetter(str) {
  //coding and coding..
  var result = [];
  var arr = str.split('');
  var alphabets = "abcdefghijklmnopqrstuvwxyz";
  for(var i = 0; i < arr.length; i++){
    if(!alphabets.includes(arr[i])){
      arr.splice(i,1);
      i--
    }
  }
  return arr.reverse().join('');
}
```



- 다른사람풀이

```
function reverseLetter(str) {
  return str.split('').reverse().filter(function(el) {if('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.indexOf(el) != -1) {
      return el;
    }
  }).join('');
}
```

음..함보쟈

오우....

나는 이렇게 썼을듯.

```
function reverseLetter(str){
	var alphabets = "abcdefghijklmnopqrstuvwxyz";
	return str.split('').reverse('').filter(function(element){
		if(alphabets.indexOf(element) !== -1){
			return element;
		}
	}).join('');
}
```

str을 음절씩 쪼개서[u,l,t,r,5,3,o,?,n]  뒤집고 [n,?,o,5,3,r,t,l,u]

filter로 거르자. element의 인덱스가 alphabets 안에 없으면 -1을 리턴하니깐. -1이 아니어야 그대로 리턴하고.

그 리턴한애들을 join('')으로 합친다.

이런거 나도 좀 써보자..ㅠㅠ

