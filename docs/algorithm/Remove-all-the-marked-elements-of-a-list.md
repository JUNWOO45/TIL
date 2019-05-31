- 문제

```
Define a method/function that removes from a given array of integers all the values contained in a second array.

Examples:
l = List()

integer_list =  [1, 1, 2 ,3 ,1 ,2 ,3 ,4]
values_list = [1, 3]
l.remove_(integer_list, values_list) == [2, 2, 4]

integer_list = [1, 1, 2 ,3 ,1 ,2 ,3 ,4, 4, 3 ,5, 6, 7, 2, 8]
lst = [1, 3, 4, 2]
l.remove_(integer_list, values_list) == [5, 6 ,7 ,8]

integer_list = [8, 2, 7, 2, 3, 4, 6, 5, 4, 4, 1, 2 , 3]
lst = [2, 4, 3]
l.remove_(integer_list, values_list) == [8, 7, 6, 5, 1]
```



- 나의풀이

```
Array.prototype.remove_ = function(integer_list, values_list){
  var result = [];
  for(var i = 0; i < integer_list.length; i++){
    if(!values_list.includes(integer_list[i])){
      result.push(integer_list[i]);
    }
  }
  return result;
}
```



- 다른사람풀이

```
Array.prototype.remove_ = function(integer_list, values_list){
  return integer_list.filter(function (element) {
    return values_list.indexOf(element) === -1;
  });
}
```

filter.

integer_list 배열안에서 filter로 걸러낸다. 그 필터는.

values_list.indexOf(element) === -1;

values_list안에 element의 인덱스는 몇인가!? 없으면 -1리턴.

즉 필터는 values_list에 없는 애들을 return하게 되고, 그 애들로 integer_list를 filter함..

풀어쓰는게 더 어렵구먼