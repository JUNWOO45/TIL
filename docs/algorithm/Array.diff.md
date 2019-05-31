6kyu

- 문제

```
Your goal in this kata is to implement a difference function, which subtracts one list from another and returns the result.

It should remove all values from list a, which are present in list b.

array_diff([1,2],[1]) == [2]
If a value is present in b, all of its occurrences must be removed from the other:

array_diff([1,2,2,2,3],[2]) == [1,3]
```



- 나의풀이

```
function array_diff(a, b) {
  var container = [];
  for(let i = 0; i < a.length; i++){
    var flag = true;
    for(let j = 0; j < b.length; j++){
      if(a[i] === b[j]){
        flag = false;
      }      
    }
    if(flag){
      container.push(a[i]);
    }
  }
  return container;
}
```



- 다른사람풀이

```
function array_diff(a, b) {
  return a.filter(function(el){return b.indexOf(el) === -1;})
}
```



확실히 활용능력의 차이다 ㅠㅠ