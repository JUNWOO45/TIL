- 문제

```


```



- 나의풀이

```
function accum(s) {
	var capital = s.toUpperCase().split("");//["A","B","C","D"]
  var count = 0;
  var result = "";
  
  for(var i = 0; i < capital.length; i++){
    result += capital[i]; // "A"
    for(var j = 0; j < count; j++){   
      result += capital[i].toLowerCase(); //"a"
    }
    result += "-";
    count++;
  }
  return result.slice(0,-1);
}
```



- 다른사람풀이

```
function accum(s) {
  return s.split('').map((c, i) => (c.toUpperCase() + c.toLowerCase().repeat(i))).join('-');
}
```

와우다 와우..

ㅠㅠ.....

s를 split으로 쪼개서 //["a", "b", "c"]

map으로 접근한다. c는 element, i는 index.

c의 대문자 + c의 소문자를 index만큼 반복하여서.

"a"의 대문자 "A" + "a"는 index가 0 이니깐 0번 반복. -> "A"

"b"의 대문자 "B" + "b"는 index가 1이니깐 1번반복 -> "Bb"

"c"의 대문자 "C" + "c"는 index가 2니깐 2번반복 -> "Ccc"



["A", "Bb", "Ccc"]를 join("-").

//"A-Bb-Ccc"

